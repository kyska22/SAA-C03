# **Día 2: IAM y Seguridad Básica - Detalle Completo**

En este segundo día, nos enfocaremos en **AWS Identity and Access Management (IAM)**, el servicio que controla el acceso a los recursos de AWS. Aprenderemos sobre usuarios, grupos, roles, políticas, MFA (Autenticación Multifactor) y cómo interactuar con AWS CLI. También realizaremos un laboratorio práctico y analizaremos un caso de uso empresarial.

---

## **1. AWS Identity and Access Management (IAM)**
IAM es el servicio de AWS que gestiona **quién (autenticación)** puede hacer **qué (autorización)** en tu cuenta de AWS.

### **a) Componentes Clave de IAM**
| **Concepto**       | **Descripción**                                                                 | **Ejemplo de Uso**                                                                 |
|--------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **Usuarios**       | Identidades (personas/apps) con credenciales únicas (nombre + contraseña/claves). | Un desarrollador necesita acceso a EC2 pero no a RDS.                             |
| **Grupos**         | Colección de usuarios con mismos permisos (mejor que asignar políticas individuales). | Equipo de "Devs" con acceso a EC2, S3 y Lambda.                                   |
| **Roles**          | Identidad temporal con permisos (usada por AWS services/EC2/lambda).            | Una instancia EC2 necesita acceso a DynamoDB.                                     |
| **Políticas**      | Documentos JSON que definen permisos (allow/deny acciones en recursos).          | Permitir solo lectura en un bucket S3 específico.                                 |

### **b) Tipos de Políticas**
- **Políticas administradas por AWS**: Predefinidas (ej: `AmazonS3ReadOnlyAccess`).  
- **Políticas personalizadas**: Creadas por el usuario para necesidades específicas.  

**Ejemplo de política JSON (solo lectura en S3):**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": ["s3:GetObject", "s3:ListBucket"],
            "Resource": ["arn:aws:s3:::mi-bucket/*", "arn:aws:s3:::mi-bucket"]
        }
    ]
}
```

---

## **2. Autenticación Multifactor (MFA)**
MFA añade una capa extra de seguridad, requiriendo **algo que sabes** (contraseña) + **algo que tienes** (código de un dispositivo).  
- **Dispositivos MFA soportados:** Google Authenticator, Authy, YubiKey.  
- **¿Dónde habilitarlo?**  
  - Usuarios IAM (recomendado para cuentas root y administradores).  
  - Operaciones sensibles (ej: borrar un bucket S3).  

**Caso de uso:**  
- Un administrador AWS debe autenticarse con MFA para cambiar políticas IAM.  

---

## **3. AWS Command Line Interface (CLI)**
La CLI de AWS permite gestionar servicios AWS desde terminal (ideal para automatización).  

### **Comandos Básicos:**
| **Comando**                     | **Descripción**                                  | **Ejemplo**                                      |
|---------------------------------|------------------------------------------------|------------------------------------------------|
| `aws configure`                | Configura credenciales AWS (access key/secret). | `aws configure` (ingresar claves de usuario IAM). |
| `aws s3 ls`                    | Listar buckets S3.                              | `aws s3 ls s3://mi-bucket`                     |
| `aws iam list-users`           | Listar usuarios IAM.                            | `aws iam list-users`                           |

---

## **4. Laboratorio: Crear Usuario IAM con Acceso S3 y Probar en AWS CLI (Paso a Paso)**
**Objetivo:** Crear un usuario IAM con permisos limitados a S3 y probar acceso desde CLI.

### **Paso 1: Crear un Usuario IAM**
1. Ingresa a la consola AWS → **IAM** → **Users** → **Add user**.  
2. Nombre de usuario: `s3-user`.  
3. Tipo de acceso: **Programmatic access** (para CLI) y **AWS Management Console** (opcional).  
4. Click en **Next: Permissions**.

### **Paso 2: Asignar Permisos S3**
1. Selecciona **Attach existing policies directly**.  
2. Busca y selecciona **AmazonS3ReadOnlyAccess** (política administrada por AWS).  
3. Click en **Next: Tags** → **Next: Review** → **Create user**.  

### **Paso 3: Guardar Credenciales**
1. Descarga el archivo `.csv` con:  
   - **Access Key ID**  
   - **Secret Access Key** (¡Guárdalas de forma segura!).  

### **Paso 4: Configurar AWS CLI**
1. Instala AWS CLI ([guía oficial](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)).  
2. Ejecuta en terminal:  
   ```bash
   aws configure
   ```
3. Ingresa:  
   - **AWS Access Key ID** y **Secret Access Key** (del paso 3).  
   - **Region:** `us-east-1` (o tu región preferida).  
   - **Output format:** `json`.  

### **Paso 5: Probar Acceso S3 desde CLI**
1. Listar buckets S3:  
   ```bash
   aws s3 ls
   ```
2. Listar archivos en un bucket (si tienes uno):  
   ```bash
   aws s3 ls s3://nombre-de-tu-bucket
   ```
3. Intentar crear un bucket (debería fallar por permisos de solo lectura):  
   ```bash
   aws s3 mb s3://bucket-no-autorizado
   ```
   - **Error esperado:** `AccessDenied`.  

---

## **5. Caso de Uso: Acceso Granular a S3 para Departamentos Empresariales**
**Escenario:** Una empresa tiene 3 departamentos (Finanzas, Marketing, Logística) que necesitan acceso diferenciado a buckets S3.  

| **Departamento** | **Requisitos de Acceso**                              | **Solución IAM**                                                                 |
|------------------|-------------------------------------------------------|---------------------------------------------------------------------------------|
| **Finanzas**     | Solo lectura en `s3://finanzas-data` (archivos confidenciales). | Política personalizada que permite `s3:GetObject` y `s3:ListBucket` solo en ese bucket. |
| **Marketing**    | Lectura/escritura en `s3://marketing-assets` (imágenes/videos). | Política con permisos `s3:*` pero solo en el bucket de marketing.                |
| **Logística**    | Acceso completo a `s3://logistics-orders`.            | Asignar la política administrada `AmazonS3FullAccess` con condición de nombre de bucket. |

**Implementación:**  
1. Crear **grupos IAM** para cada departamento (`Finanzas-Group`, `Marketing-Group`, etc.).  
2. Asignar políticas personalizadas a cada grupo.  
3. Añadir usuarios a los grupos según su departamento.  

**Beneficios:**  
- **Seguridad:** Evita acceso no autorizado a datos sensibles.  
- **Auditoría:** Cada acción queda registrada en **AWS CloudTrail**.  

---

## **Resumen del Día 2**
✅ **Conceptos clave:** Usuarios, grupos, roles, políticas IAM, MFA, AWS CLI.  
✅ **Laboratorio:** Creación de usuario IAM con acceso S3 y prueba en CLI.  
✅ **Caso de uso:** Control de acceso granular para buckets S3 en una empresa.  

**Siguientes pasos:** En el **Día 3** trabajaremos con **EC2 y Elastic Block Store (EBS)**, lanzando instancias y configurando almacenamiento.  
