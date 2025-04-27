# **Día 3: EC2 y Elastic Block Store (EBS) - Detalle Completo**

En este tercer día, nos adentraremos en **Amazon EC2 (Elastic Compute Cloud)**, el servicio fundamental de AWS para computación en la nube. Aprenderemos sobre tipos de instancias, AMIs, almacenamiento (EBS vs. Instance Store) y grupos de seguridad. Realizaremos un laboratorio práctico y analizaremos un caso de uso de hosting web con persistencia de datos.

---

## **1. Amazon EC2: Conceptos Clave**

### **a) Tipos de Instancias EC2**
AWS ofrece múltiples familias de instancias optimizadas para diferentes cargas de trabajo:

| **Familia**       | **Optimización**          | **Ejemplo de Uso**                              | **Instancia Ejemplo** |
|--------------------|--------------------------|-----------------------------------------------|----------------------|
| **General Purpose** | Balanceadas (CPU/memoria) | Aplicaciones web, servidores pequeños.         | `t3.micro`, `m5.large` |
| **Compute Optimized** | Alto rendimiento CPU    | Procesamiento batch, servidores de juegos.     | `c5.xlarge`          |
| **Memory Optimized** | Grandes cargas en RAM   | Bases de datos en memoria (Redis).             | `r5.2xlarge`         |
| **Storage Optimized** | Alto I/O de disco      | Data warehouses (Apache Hadoop).               | `i3.4xlarge`         |
| **GPU Optimized**    | Procesamiento gráfico  | Machine Learning, renderizado 3D.              | `p3.8xlarge`         |

**Ejemplo:**  
- Un sitio web con tráfico moderado usa `t3.micro` (económica, buen rendimiento).  
- Un servidor de análisis de datos requiere `r5.2xlarge` (128 GB RAM).  

---

### **b) AMIs (Amazon Machine Images)**
Una AMI es una "plantilla" preconfigurada para lanzar instancias EC2 (SO, software, configuraciones).  

| **Tipo de AMI**      | **Descripción**                              | **Ejemplo de Uso**                          |
|----------------------|--------------------------------------------|--------------------------------------------|
| **Amazon Linux 2**   | SO optimizado para AWS (gratis).           | Servidores genéricos, desarrollo.          |
| **Ubuntu Server**    | Popular para entornos DevOps.              | Docker, Kubernetes.                        |
| **Windows Server**   | Para aplicaciones .NET o Active Directory. | ERP corporativo (SAP, Dynamics).           |
| **AMIs Personalizadas** | Creadas por usuarios desde instancias EC2. | Empresa que necesita una imagen con software preinstalado. |

**Ejemplo:**  
- Un equipo DevOps usa una AMI con Docker preinstalado para desplegar contenedores rápidamente.  

---

### **c) Almacenamiento en EC2: EBS vs. Instance Store**
| **Característica**       | **EBS (Elastic Block Store)**               | **Instance Store (Ephemeral Storage)**      |
|--------------------------|--------------------------------------------|--------------------------------------------|
| **Persistencia**         | Sí (sobrevive al apagado de la instancia). | No (se borra al detener/terminar la instancia). |
| **Rendimiento**          | Bueno (mejor con tipos provisioned IOPS).  | Excelente (baja latencia, ideal para cache). |
| **Escalabilidad**        | Puede redimensionarse (aumentar tamaño).   | Fijo (depende del tipo de instancia).      |
| **Caso de uso típico**   | Bases de datos, sistemas de archivos.      | Caché temporal, buffers de alta velocidad. |

**Ejemplo:**  
- Una base de datos MySQL usa **EBS** para persistencia.  
- Un servidor de videojuegos usa **Instance Store** para caché de texturas.  

---

### **d) Security Groups (Grupos de Seguridad)**
Son firewalls virtuales que controlan el tráfico entrante/saliente de las instancias EC2.  

| **Regla Típica**          | **Protocolo/Puerto** | **Origen/Destino**       | **Ejemplo de Uso**                     |
|--------------------------|---------------------|-------------------------|---------------------------------------|
| **HTTP (Web)**          | TCP 80              | 0.0.0.0/0 (todo internet). | Permitir acceso a un sitio web.       |
| **SSH (Administración)** | TCP 22              | Mi IP pública.           | Acceso remoto seguro a la instancia.  |
| **HTTPS (Seguro)**      | TCP 443             | 0.0.0.0/0.               | Sitio web con SSL/TLS.                |

**Ejemplo:**  
- Un Security Group para WordPress permite tráfico HTTP/HTTPS y SSH solo desde tu IP.  

---

## **2. Laboratorio: Lanzar una Instancia EC2 con EBS (Paso a Paso)**
**Objetivo:** Lanzar una instancia EC2 con Linux, conectarse via SSH y montar un volumen EBS adicional.

### **Paso 1: Lanzar una Instancia EC2**
1. En la consola AWS, ve a **EC2** → **Launch Instance**.  
2. Elige una AMI: **Amazon Linux 2 AMI** (gratis en Free Tier).  
3. Selecciona un tipo de instancia: **t2.micro** (Free Tier eligible).  
4. Configura detalles:  
   - **Número de instancias:** 1.  
   - **Red:** Default VPC.  
   - **Subnet:** Cualquier disponibilidad.  
5. Agrega almacenamiento:  
   - **Root volume:** 8 GB (EBS gp2).  
   - **Add New Volume:** +10 GB (EBS gp2) para datos.  
6. Configura Security Group:  
   - **Nombre:** `web-server-sg`.  
   - **Reglas:**  
     - SSH (TCP 22) → **Your IP**.  
     - HTTP (TCP 80) → **0.0.0.0/0**.  
7. **Review and Launch** → **Launch**.  
8. **Crear un par de claves** (o usar existente):  
   - Nombre: `ec2-keypair`.  
   - Descargar `.pem` (¡Guárdalo en un lugar seguro!).  

### **Paso 2: Conectarse a la Instancia via SSH**
1. En **EC2 Dashboard**, selecciona la instancia → **Connect**.  
2. Sigue las instrucciones para SSH (ejemplo en Linux/macOS):  
   ```bash
   chmod 400 ec2-keypair.pem  # Permisos seguros para la clave.
   ssh -i ec2-keypair.pem ec2-user@<IP-PÚBLICA-EC2>
   ```
3. ¡Conectado! Verás el prompt de Amazon Linux.  

### **Paso 3: Montar un Volumen EBS Adicional**
1. Dentro de la instancia, lista los discos disponibles:  
   ```bash
   lsblk
   ```
   - Verás `xvdf` (el volumen EBS de 10 GB añadido).  
2. Formatea el disco (si es nuevo):  
   ```bash
   sudo mkfs -t ext4 /dev/xvdf
   ```
3. Crea un directorio y monta el disco:  
   ```bash
   sudo mkdir /mnt/datos
   sudo mount /dev/xvdf /mnt/datos
   ```
4. Verifica el montaje:  
   ```bash
   df -h
   ```
   - Debe mostrar `/mnt/datos` con 10 GB.  

### **Paso 4 (Opcional): Hacer el Montaje Persistente**
1. Edita `/etc/fstab` para montar automáticamente al reiniciar:  
   ```bash
   echo "/dev/xvdf /mnt/datos ext4 defaults,nofail 0 2" | sudo tee -a /etc/fstab
   ```

---

## **3. Ejemplo: Hosting de una Aplicación Web con Almacenamiento Persistente**
**Escenario:** Desplegar un sitio web estático en EC2 con EBS para almacenar contenido.  

### **Arquitectura Propuesta:**
1. **Instancia EC2:** `t3.micro` con Amazon Linux 2.  
2. **Almacenamiento:**  
   - **EBS Root Volume (8 GB):** SO y software (Apache/Nginx).  
   - **EBS Adicional (10 GB):** Directorio `/var/www/html` (contenido web).  
3. **Security Group:** Permite HTTP (80) y SSH (22).  

### **Pasos Adicionales (Post-Lab):**
1. Instalar Apache:  
   ```bash
   sudo yum install httpd -y
   sudo systemctl start httpd
   ```
2. Mover el contenido web al EBS montado:  
   ```bash
   sudo mv /var/www/html /mnt/datos/html
   sudo ln -s /mnt/datos/html /var/www/html
   ```
3. Acceder al sitio web via navegador:  
   - Abre `http://<IP-PÚBLICA-EC2>`.  

**Beneficios:**  
- Si la instancia falla, los datos persisten en EBS (puede reattacharse a otra instancia).  
- Escalable: Aumenta el tamaño del EBS sin downtime.  

---

## **Resumen del Día 3**
✅ **Conceptos clave:** Tipos de instancias, AMIs, EBS vs. Instance Store, Security Groups.  
✅ **Laboratorio:** Lanzar EC2, conectar via SSH y montar EBS.  
✅ **Ejemplo práctico:** Hosting web con persistencia en EBS.  

**Siguientes pasos:** En el **Día 4** exploraremos **Elastic Load Balancing (ELB) y Auto Scaling Groups (ASG)** para aplicaciones escalables.  
