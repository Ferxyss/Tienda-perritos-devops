# Innovatech - Evaluación 3 DevOps

## Descripción

Este proyecto corresponde a la Evaluación 3 de DevOps, cuyo objetivo es implementar una plataforma contenerizada desplegada en AWS utilizando Kubernetes (EKS), Amazon ECR y GitHub Actions para automatizar el proceso de integración y despliegue continuo (CI/CD).

La solución implementa una aplicación de gestión de tienda compuesta por:

- Frontend
- Backend
- Base de datos MySQL

Todos los componentes son desplegados en un clúster Amazon EKS y administrados mediante Kubernetes.

---

# Arquitectura

```text
GitHub
   │
   ▼
GitHub Actions
   │
   ├── Build Frontend
   ├── Build Backend
   ├── Build Database
   │
   ▼
Amazon ECR
   │
   ▼
Amazon EKS
   │
   ├── Frontend Deployment
   ├── Backend Deployment
   ├── MySQL Deployment
   │
   ▼
LoadBalancer
```

---

# Tecnologías utilizadas

## Cloud

- AWS EKS
- AWS ECR
- AWS IAM
- AWS VPC
- AWS Load Balancer

## DevOps

- GitHub Actions
- Docker
- Kubernetes
- Horizontal Pod Autoscaler (HPA)

## Aplicación

### Frontend

- HTML
- JavaScript
- Nginx

### Backend

- Node.js
- Express

### Base de datos

- MySQL

---

# Estructura del proyecto

```text
.
├── backend/
├── frontend/
├── db/
├── k8s/
│   ├── namespace.yaml
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── backend-hpa.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   ├── frontend-hpa.yaml
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   └── mysql-secret.yaml
│
├── deploy.sh
└── README.md
```

---

# Contenedores

La aplicación está compuesta por tres imágenes Docker:

| Componente | Repositorio ECR |
|------------|----------------|
| Frontend | tienda-frontend |
| Backend | tienda-backend |
| Database | tienda-db |

---

# Cluster Kubernetes

Se implementó un clúster Amazon EKS con:

- Node Group administrado
- LoadBalancer para acceso externo
- Namespace dedicado
- Despliegue de frontend, backend y base de datos
- Escalamiento automático mediante HPA

---

# Autoscaling (HPA)

## Frontend

- Mínimo: 2 Pods
- Máximo: 6 Pods
- CPU objetivo: 60%

## Backend

- Mínimo: 2 Pods
- Máximo: 10 Pods
- CPU objetivo: 70%

---

# Pipeline CI/CD

El pipeline se ejecuta automáticamente mediante GitHub Actions al realizar un push sobre la rama principal.

## Etapas

### 1. Build

Construcción automática de:

- Frontend
- Backend
- Base de datos

### 2. Push

Publicación de imágenes Docker en Amazon ECR.

### 3. Deploy

Despliegue automático en Amazon EKS utilizando Kubernetes.

### 4. Validación

Verificación de:

- Deployments
- Services
- Pods
- HPA

---

# Secrets utilizados

El pipeline utiliza Secrets de GitHub para conectarse a AWS.

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_SESSION_TOKEN
AWS_REGION
```

---

# Flujo de despliegue

```text
Push a GitHub
        │
        ▼
GitHub Actions
        │
        ▼
Build Docker Images
        │
        ▼
Push Amazon ECR
        │
        ▼
Deploy Amazon EKS
        │
        ▼
Verificación Kubernetes
```

---

# Validaciones realizadas

Se verificó:

- Correcta construcción de imágenes Docker.
- Publicación de imágenes en Amazon ECR.
- Despliegue automático en Amazon EKS.
- Funcionamiento del frontend.
- Comunicación Frontend → Backend.
- Disponibilidad de la base de datos.
- Funcionamiento de HPA.
- Correcta ejecución del pipeline CI/CD.

---

# Evidencias

Durante la evaluación se obtuvieron evidencias de:

- Creación del clúster EKS.
- Repositorios ECR.
- Ejecución de GitHub Actions.
- Deployments Kubernetes.
- Pods en ejecución.
- Servicios y LoadBalancer.
- Configuración de HPA.

---

# Autor

Fernanda Paredes

Evaluación 3 - DevOps
Innovatech Chile
