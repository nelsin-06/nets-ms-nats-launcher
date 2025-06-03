# Microservices Store

A store application built with microservices architecture using NestJS, NATS as message broker, and Docker for orchestration. The project is divided into multiple independent microservices that communicate through asynchronous messaging.

## 🚀 Quick Start - API Testing

Test our API endpoints using the Postman collection. Choose your preferred option. 


:warning: **No matter which option is selected, you'll need to choose one environment when testing this API. We recommend selecting documentation_endpoint_production if you only want to test our API. However, if you are running the API locally, select documentation_endpoint_develop**:

### Fork Collection
Import the collection directly into your Postman workspace with pre-configured environment variables:

[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/22972674-1f275a2d-a95f-4172-98d3-7e760552968c?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D22972674-1f275a2d-a95f-4172-98d3-7e760552968c%26entityType%3Dcollection%26workspaceId%3D460997b1-e9ef-42f7-861d-9f7ba852ab55#?env%5Bdocumentation_endpoint_production%5D=W3sia2V5IjoidXJsIiwidmFsdWUiOiJodHRwczovL3N0b3JlLm1zLjM0LjguNzMuMTMyLm5pcC5pby9hcGkiLCJlbmFibGVkIjp0cnVlLCJ0eXBlIjoiZGVmYXVsdCJ9LHsia2V5IjoicHJvZHVjdElkIiwidmFsdWUiOiIxNCIsImVuYWJsZWQiOnRydWUsInR5cGUiOiJkZWZhdWx0In0seyJrZXkiOiJvcmRlcklkIiwidmFsdWUiOiIzODIzNjk2Ny0wOWYzLTRhOTgtYTgyMi1mMjZlMjhlODI3NjciLCJlbmFibGVkIjp0cnVlLCJ0eXBlIjoiZGVmYXVsdCJ9LHsia2V5Ijoic3RhdHVzT3JkZXIiLCJ2YWx1ZSI6IkRFTElWRVJFRCIsImVuYWJsZWQiOnRydWUsInR5cGUiOiJkZWZhdWx0In0seyJrZXkiOiJ0b2tlbiIsInZhbHVlIjoiPEpTT05fV0VCX1RPS0VOPiIsImVuYWJsZWQiOnRydWUsInR5cGUiOiJhbnkifSx7ImtleSI6InVybF93ZWJob29rX3BheW1lbnQiLCJ2YWx1ZSI6InN0b3JlLm1zLjM0LjExNy4yNTAuMjEyLm5pcC5pbyIsImVuYWJsZWQiOnRydWUsInR5cGUiOiJkZWZhdWx0In0seyJrZXkiOiJ1cmxfd2ViaG9va19jbGllbnQiLCJ2YWx1ZSI6InN0b3JlLm1zLjM0LjguNzMuMTMyLm5pcC5pbyIsImVuYWJsZWQiOnRydWUsInR5cGUiOiJkZWZhdWx0In1d)

### View Collection Online
Browse the collection documentation and endpoints directly in your browser:

[<img src="https://img.shields.io/badge/View%20in-Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white" alt="View In Postman">](https://www.postman.com/dark-equinox-132990/nest/collection/pmibtaz/store-ms)

## Arquitectura del Proyecto

Este repositorio principal contiene la configuración de orquestación para todos los microservicios de la tienda. Cada microservicio está almacenado en un repositorio separado dentro de la organización `nest-microservices-nel` y se incluye como git submodule:

- **client-gateway**: Gateway principal que expone las APIs REST
- **products-ms**: Microservicio de gestión de productos
- **orders-ms**: Microservicio de gestión de órdenes
- **payments-s**: Microservicio de pagos (integración con Stripe)
- **auth-mss**: Microservicio de autenticación y autorización

## Instalación y Configuración

### 1. Clonar el Repositorio

```bash
git clone https://github.com/nelsin-06/nets-ms-nats-launcher.git
cd nets-ms-nats-launcher
```


### 2. Descargar Submódulos

```bash
git submodule update --init --recursive
```


### 3. Configurar Variables de Entorno

Crea un archivo `.env` basado en `.env.template`:

```bash
cp .env.template .env
```


**Variables requeridas:**
- `PORT_CLIENT_GATEWAY_HOST`: Puerto del gateway (por defecto: 8080)
- `DATABASE_MONGO_URL`: URL de conexión a MongoDB para auth-ms
- `STRIPE_SECRET`: Clave secreta de Stripe
- `STRIPE_SIGNING_WEBHOOK_ENDPOINT`: Endpoint de webhook de Stripe
- `JWT_SECRET`: Secreto para tokens JWT

## Project Execution (use the production option if you want to run the project using the Docker image from the cloud)


### Producción

```bash
docker compose -f docker-compose.prod.yml up --build
```

### Desarrollo con Docker Compose

```bash
docker compose up --build
```

**Nota:** En desarrollo, algunos microservicios están comentados en el docker-compose.yml para facilitar el desarrollo individual.

## Configuración de Kubernetes

El proyecto incluye configuraciones completas para despliegue en Kubernetes usando Helm charts ubicadas en `k8s/store-ms/`.

### Estructura de K8s

```
k8s/store-ms/
├── Chart.yaml              # Configuración del Helm chart
├── values.yaml             # Valores por defecto
└── templates/              # Manifiestos de Kubernetes
    ├── auth-ms/
    ├── client-gateway/
    ├── orders-ms/
    ├── payments-ms/
    ├── products-ms/
    ├── nats/
    └── ingress/
```

### Despliegue en Kubernetes

1. **Crear secretos necesarios:**
```bash
kubectl create secret generic auth-ms-secrets \
  --from-literal=DATABASE_MONGO_URL="<mongo-url>" \
  --from-literal=JWT_SECRET="<jwt-secret>"

kubectl create secret generic orders-ms-secrets \
  --from-literal=DATABASE_URL="<postgres-url>"

kubectl create secret generic payments-ms-secrets \
  --from-literal=STRIPE_SECRET="<stripe-secret>" \
  --from-literal=STRIPE_SIGNING_WEBHOOK_ENDPOINT="<webhook-endpoint>"
```

2. **Configure Google Container Registry access (Production only):**
> **Note**: This step is only required for production deployment with private container registry access. Skip this if you're testing locally or don't have access to the private registry.

```bash
# Only for production with private registry access
kubectl create secret docker-registry gcr-json-key \
  --docker-server=southamerica-east1-docker.pkg.dev \
  --docker-username=_json_key \
  --docker-password="$(cat path/to/service-account.json)" \
  --docker-email=your-email@gmail.com

kubectl patch serviceaccounts default -p '{"imagePullSecrets": [{"name":"gcr-json-key"}]}'
```

3. **Desplegar con Helm:**
```bash
# Instalación inicial
helm install store-ms k8s/store-ms/

# Actualizaciones
helm upgrade store-ms k8s/store-ms/
```

### Características de la Configuración K8s

- **Ingress con SSL**: Certificados SSL automáticos para los dominios configurados
- **Persistent Volumes**: Para persistencia de datos del products-ms (SQLite)
- **Resource Limits**: Configuración de límites de CPU y memoria
- **Health Checks**: Liveness y readiness probes configurados
- **Secrets Management**: Variables sensibles manejadas como Kubernetes secrets

## Comandos Útiles

### Git Submodules
```bash
# Actualizar todos los submódulos a la última versión
git submodule update --remote

# Actualizar un submódulo específico
git submodule update --remote <submodule-name>
```

### Kubernetes
```bash
# Ver estado de pods
kubectl get pods

# Ver logs de un pod
kubectl logs <pod-name>

# Ver servicios
kubectl get services

# Ver ingress
kubectl get ingress
```

## Importante

Al trabajar con submódulos, siempre **actualiza y haz push primero en el submódulo** y **después en el repositorio principal**. Si se hace en orden inverso, se perderán las referencias de los submódulos.

## URLs de Acceso

- **Desarrollo**: http://localhost:8080
- **Producción K8s**: Configurado via Ingress (ver archivos de ingress para URLs específicas)
