# **Día 1: Introducción a AWS y Cloud Computing - Detalle Completo**

En este primer día, nos enfocaremos en los fundamentos de AWS y cloud computing, incluyendo los modelos de servicio, el modelo de responsabilidad compartida y la infraestructura global de AWS (Regiones y Zonas de Disponibilidad). También realizaremos un laboratorio práctico de creación de una cuenta AWS y compararemos el despliegue de una aplicación en **on-premise** vs. **AWS**.

---

## **1. Modelos de Cloud Computing (IaaS, PaaS, SaaS)**
AWS ofrece diferentes modelos de servicio en la nube, cada uno con distintos niveles de control y administración:

### **a) Infrastructure as a Service (IaaS)**
- **Definición:** AWS proporciona infraestructura básica (servidores, almacenamiento, redes), pero el usuario gestiona el SO, middleware y aplicaciones.
- **Ejemplos de AWS:** EC2, EBS, VPC.
- **Caso de uso:**  
  - Una empresa migra sus servidores físicos a instancias EC2 para evitar el mantenimiento de hardware.  
  - Un desarrollador despliega una aplicación web en EC2 con su propia configuración de servidor (Apache/Nginx).

### **b) Platform as a Service (PaaS)**
- **Definición:** AWS gestiona el sistema operativo y middleware, mientras el usuario solo se enfoca en desarrollar y desplegar aplicaciones.
- **Ejemplos de AWS:** Elastic Beanstalk, RDS, Lambda.  
- **Caso de uso:**  
  - Un equipo de desarrollo despliega una aplicación en Elastic Beanstalk sin preocuparse por la infraestructura subyacente.  
  - Una startup usa Aurora (RDS) para su base de datos sin administrar servidores SQL.

### **c) Software as a Service (SaaS)**
- **Definición:** AWS provee aplicaciones completas gestionadas, accesibles vía web.
- **Ejemplos de AWS:** Amazon WorkMail, Chime (aunque AWS no es principalmente un proveedor SaaS).  
- **Caso de uso externo (no AWS):**  
  - Una empresa usa **Salesforce** (CRM) o **Slack** (mensajería) sin instalar software local.

---

## **2. Modelo de Responsabilidad Compartida**
AWS y el cliente comparten la seguridad de la siguiente manera:

| **Responsabilidad de AWS** | **Responsabilidad del Cliente** |
|----------------------------|----------------------------------|
| Seguridad física de los data centers | Configuración de seguridad (IAM, Security Groups) |
| Mantenimiento de hardware | Gestión de parches en instancias EC2 |
| Redundancia global (Regiones/AZs) | Copias de seguridad (backups) de datos |
| Cumplimiento de certificaciones (ISO, SOC) | Encriptación de datos sensibles |

**Ejemplo:**  
- Si un hacker explota una vulnerabilidad en una instancia EC2 por falta de parches, es responsabilidad del cliente.  
- Si hay un fallo eléctrico en un data center de AWS, es responsabilidad de AWS garantizar la redundancia.

---

## **3. Regiones y Zonas de Disponibilidad (AZs)**
### **a) Regiones AWS**
- Son ubicaciones geográficas donde AWS tiene data centers (ej: **us-east-1** en Virginia, **eu-west-1** en Irlanda).  
- Cada región está completamente aislada para alta disponibilidad y cumplimiento legal (GDPR, HIPAA).  

**Ejemplo:**  
- Una empresa europea elige **eu-central-1** (Frankfurt) para cumplir con GDPR.  
- Un servicio global usa **CloudFront** para distribuir contenido cerca de los usuarios.

### **b) Zonas de Disponibilidad (AZs)**
- Son centros de datos independientes dentro de una región (ej: **us-east-1a**, **us-east-1b**).  
- Diseñadas para tolerancia a fallos (si una AZ falla, otras siguen operativas).  

**Ejemplo:**  
- Una aplicación crítica despliega servidores en **us-east-1a** y **us-east-1b** para alta disponibilidad.  
- Una base de datos RDS en Multi-AZ replica datos en otra AZ automáticamente.

---

## **4. Laboratorio: Crear una Cuenta AWS (Paso a Paso)**
**Objetivo:** Configurar una cuenta AWS Free Tier para prácticas sin costo (12 meses gratis).

### **Paso 1: Registro en AWS**
1. Ingresa a [https://aws.amazon.com/](https://aws.amazon.com/) y haz clic en **"Crear una cuenta AWS"**.
2. Proporciona un correo electrónico, nombre y contraseña.
3. Verifica tu correo con el código enviado por AWS.

### **Paso 2: Datos de Pago**
1. Ingresa los datos de una tarjeta de crédito (no se cobrará nada a menos que excedas el Free Tier).  
2. AWS hará una verificación con un cargo temporal de ~$1 (reembolsable).

### **Paso 3: Seleccionar Plan de Soporte**
1. Elige el plan **"Basic"** (gratuito).  
2. Completa el proceso de verificación de identidad (puede requerir llamada o SMS).

### **Paso 4: Acceder a la Consola AWS**
1. Inicia sesión en [https://console.aws.amazon.com/](https://console.aws.amazon.com/).  
2. Explora la consola y familiarízate con los servicios.

---

## **5. Ejemplo: Comparación On-Premise vs. AWS**
### **Escenario:** Despliegue de una aplicación web (WordPress).

| **Aspecto** | **On-Premise** | **AWS** |
|-------------|----------------|---------|
| **Infraestructura** | Compra de servidores físicos. | Uso de EC2 bajo demanda (pago por hora). |
| **Escalabilidad** | Limitada por hardware físico. | Auto Scaling ajusta capacidad según tráfico. |
| **Tiempo de despliegue** | Semanas para comprar/configurar servidores. | Minutos para lanzar instancias EC2. |
| **Costo inicial** | Alto (CAPEX: servidores, licencias). | Bajo (OPEX: pago por uso). |
| **Alta disponibilidad** | Requiere balanceadores y clusters costosos. | ELB + Multi-AZ incluidos en AWS. |
| **Mantenimiento** | Equipo de TI interno necesario. | AWS gestiona hardware y red. |

**Conclusión:** AWS reduce costos iniciales, mejora escalabilidad y elimina la necesidad de gestionar infraestructura física.

---

## **Resumen del Día 1**
✅ **Conceptos clave:** IaaS, PaaS, SaaS, responsabilidad compartida, Regiones/AZs.  
✅ **Laboratorio:** Creación de cuenta AWS Free Tier.  
✅ **Ejemplo práctico:** Comparación on-premise vs. AWS para WordPress.  

**Siguientes pasos:** En el **Día 2** exploraremos **IAM (Identity and Access Management)** para gestionar seguridad en AWS.  
