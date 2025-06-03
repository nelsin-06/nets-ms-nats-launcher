# Microservices Store

Una aplicación de tienda construida con arquitectura de microservicios usando NestJS, NATS como message broker y Docker para orquestación. El proyecto está dividido en múltiples microservicios independientes que se comunican a través de mensajería asíncrona.

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
git clone <repository-url>
cd <repository-name>
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

## Ejecución del Proyecto

### Desarrollo con Docker Compose

```bash
docker compose up --build
```

### Producción

```bash
docker compose -f docker-compose.prod.yml up --build
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

2. **Configurar acceso a Google Container Registry:**
```bash
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
