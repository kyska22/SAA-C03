# **Cronograma de Estudio para AWS Certified Solutions Architect - Associate (4 semanas, 40 min/día, sin domingos)**

## **Semana 1: Fundamentos de AWS y Servicios Básicos**
**Objetivo:** Comprender los conceptos básicos de AWS, la infraestructura global y los servicios esenciales.

### **Día 1: Introducción a AWS y Cloud Computing**
- **Temas:** Modelos de cloud (IaaS, PaaS, SaaS), responsabilidad compartida, regiones y AZs.
- **Laboratorio:** Crear una cuenta AWS (usar AWS Free Tier o Sandbox de Whizlabs).
- **Ejemplo:** Comparar el despliegue de una app en on-premise vs. AWS.

### **Día 2: IAM y Seguridad Básica**
- **Temas:** IAM (usuarios, grupos, roles, políticas), MFA, CLI.
- **Laboratorio:** Crear un usuario IAM con permisos S3 y probar acceso desde AWS CLI.
- **Caso de uso:** Empresa que necesita acceso granular a buckets S3 para diferentes departamentos.

### **Día 3: EC2 y Elastic Block Store (EBS)**
- **Temas:** Tipos de instancias, AMIs, almacenamiento (EBS vs. Instance Store), Security Groups.
- **Laboratorio:** Lanzar una instancia EC2 con Linux, conectarse via SSH y montar un volumen EBS.
- **Ejemplo:** Hosting de una aplicación web en una instancia EC2 con almacenamiento persistente.

### **Día 4: Balanceo de Carga y Escalabilidad (ELB & ASG)**
- **Temas:** ALB, NLB, Auto Scaling Groups (ASG), políticas de escalado.
- **Laboratorio:** Configurar un ALB con dos instancias EC2 y un ASG basado en CPU.
- **Caso de uso:** Sitio de e-commerce que escala en temporada alta.

### **Día 5: S3 y CloudFront**
- **Temas:** Clases de almacenamiento, versionado, lifecycle policies, CDN.
- **Laboratorio:** Subir archivos a S3, habilitar versionado y configurar CloudFront.
- **Ejemplo:** Distribución global de archivos estáticos para una aplicación web.

### **Día 6: Bases de Datos (RDS & DynamoDB)**
- **Temas:** RDS (Multi-AZ, Read Replicas), DynamoDB (RCU/WCU, índices).
- **Laboratorio:** Crear una instancia RDS MySQL y una tabla en DynamoDB.
- **Caso de uso:** Base de datos para una app con alta disponibilidad vs. NoSQL para alta escalabilidad.

---

## **Semana 2: Redes, Seguridad Avanzada y Serverless**
**Objetivo:** Dominar VPC, seguridad avanzada y servicios serverless.

### **Día 7: Amazon VPC (Fundamentos)**
- **Temas:** Subnets públicas/privadas, Internet Gateway, NAT Gateway.
- **Laboratorio:** Crear una VPC con subnets públicas/privadas y probar conectividad.
- **Ejemplo:** Arquitectura de 3 capas (web, app, DB) en una VPC.

### **Día 8: VPC Avanzado (Peering, Endpoints, VPN)**
- **Temas:** VPC Peering, Endpoints (S3, DynamoDB), VPN y Direct Connect.
- **Laboratorio:** Configurar VPC Peering entre dos VPCs y un Endpoint S3.
- **Caso de uso:** Empresa con múltiples entornos (dev/prod) que comparten recursos.

### **Día 9: Seguridad Avanzada (KMS, Secrets Manager, WAF)**
- **Temas:** Encriptación (KMS), gestión de secretos, WAF y Shield.
- **Laboratorio:** Encriptar un bucket S3 con KMS y configurar WAF para bloquear tráfico malicioso.
- **Ejemplo:** Aplicación financiera que requiere encriptación y protección DDoS.

### **Día 10: Lambda y API Gateway**
- **Temas:** Serverless, triggers, políticas IAM para Lambda.
- **Laboratorio:** Crear una Lambda que se ejecute al subir un archivo a S3 y exponerla via API Gateway.
- **Caso de uso:** Procesamiento de imágenes sin servidores (ej: thumbnails al subir fotos).

### **Día 11: SQS, SNS y EventBridge**
- **Temas:** Mensajería (SQS vs. SNS), EventBridge para eventos.
- **Laboratorio:** Configurar un flujo S3 → SNS → Lambda → DynamoDB.
- **Ejemplo:** Notificaciones en tiempo real para una app de pedidos.

### **Día 12: AWS Step Functions**
- **Temas:** Flujos de trabajo con Step Functions.
- **Laboratorio:** Crear un flujo de aprobación manual para un proceso de pedidos.
- **Caso de uso:** Automatización de procesos empresariales (ej: onboarding de empleados).

---

## **Semana 3: Arquitecturas Avanzadas y Migración**
**Objetivo:** Diseñar arquitecturas escalables y entender estrategias de migración.

### **Día 13: High Availability & Disaster Recovery**
- **Temas:** RTO/RPO, backups, pilot light, warm standby.
- **Laboratorio:** Configurar RDS Multi-AZ y replicación entre regiones.
- **Ejemplo:** Plan de recuperación ante desastres para una app crítica.

### **Día 14: Docker & ECS/EKS**
- **Temas:** Contenedores, ECS (Fargate), EKS.
- **Laboratorio:** Desplegar un contenedor Docker en ECS Fargate.
- **Caso de uso:** Migración de una app monolítica a microservicios.

### **Día 15: AWS Organizations & Control Tower**
- **Temas:** Multi-cuenta, SCPs, Control Tower.
- **Laboratorio:** Configurar una organización con políticas SCP.
- **Ejemplo:** Empresa con equipos de desarrollo y producción separados.

### **Día 16: Migración (AWS DMS, Snowball)**
- **Temas:** Database Migration Service (DMS), Snowball.
- **Laboratorio:** Migrar una base de datos local (simulada en EC2) a RDS con DMS.
- **Caso de uso:** Migración de una base de datos SQL Server a Aurora.

### **Día 17: Cost Optimization & Well-Architected Framework**
- **Temas:** Reservas, Savings Plans, Trusted Advisor.
- **Laboratorio:** Analizar costos con AWS Cost Explorer y recomendar optimizaciones.
- **Ejemplo:** Reducción de costos en una startup con instancias subutilizadas.

### **Día 18: Repaso y Simulacro de Examen**
- **Actividad:** Tomar un examen de práctica (Whizlabs o Udemy).
- **Enfoque:** Identificar áreas débiles para repasar en la última semana.

---

## **Semana 4: Repaso Final y Simulacros**
**Objetivo:** Consolidar conocimientos y practicar con exámenes simulados.

### **Días 19-24: Repaso y Simulacros Diarios**
- **Día 19:** Repaso de EC2, ASG, ELB + simulacro (20 preguntas).
- **Día 20:** Repaso de S3, CloudFront, Storage Gateway + simulacro.
- **Día 21:** Repaso de RDS, DynamoDB, Redshift + casos de uso.
- **Día 22:** Repaso de Serverless (Lambda, API Gateway, Step Functions).
- **Día 23:** Repaso de Seguridad (IAM, KMS, WAF) + mejores prácticas.
- **Día 24:** Examen final de simulación (65 preguntas, tiempo limitado).

---

## **Recomendaciones Finales**
1. **Laboratorios clave:**  
   - Desplegar una arquitectura de 3 capas (web, app, DB).  
   - Configurar alta disponibilidad con Multi-AZ y Auto Scaling.  
   - Automatizar con CloudFormation o Terraform (opcional).  
2. **Enfoque en casos de uso:**  
   - Startups que necesitan escalabilidad.  
   - Empresas con requerimientos de compliance (HIPAA, GDPR).  
   - Migración de legacy systems a la nube.  
3. **Recursos:**  
   - **Whizlabs Sandbox:** Usar sus laboratorios prácticos.  
   - **AWS Free Tier:** Para pruebas reales sin costo.  
   - **Exámenes de práctica:** Jon Bonso (Udemy) y AWS Official Practice Exam.  
