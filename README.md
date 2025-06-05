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

## Project Architecture

### 🏗️ Store MS - Architecture Flow

[![Store MS Architecture Diagram](https://github.com/nelsin-06/nets-ms-nats-launcher/blob/main/diagram.png)]([https://www.mermaidchart.com/app/projects/81245b59-1bcd-440e-9f38-4a6c604611a9/diagrams/5d07c0aa-247f-4ffe-be54-647218364dc0/version/v0.1/view](https://mermaid.live/edit#pako:eNqNWFuP28YV_isDBnkqpYg3iSsUAbSiolW9F1WSk6Z1saCoocQuRaq8rL01DCRAnoqkdmwDblMUbosiNfLQPuShAfpv8gfqn9AzV5Ej7coLiKv5eM43M-ecOeeMHmtBusBaVwvj9GGw8rMCzbwHCYK_999HHr7GcbpZ46RA45WfY_YG4F890N6-_vrNj5999fb18_8CkvtZlsZxik7TwI8faL9GjcaHaBgVVPLlF-QrGpf5Cvlo7UcJSDAyORkInJRzNMGbNI-KNItwjqZFVgZFmfGJ83K-zPzNCg1Hs5P7x5cXkyGlf_p3lOC8aKyjIEtznF1HAc4bCY7lLORveGJQ6RefoyCOYE-NpV_gh_7NT-fZBx--ff3lM9Qbj9CQgYqqKVT9slg11jnXeQk6AABZFPhFlCaKmiXUNv4NMWPeEJrPv0djjik6ttBJswXOtnP9-Tm6IIgq78g5snQB5sq3Ki--RWMOSiWcLKqWlzY9643OLyeD8QUz6V_RGbhp6w7VIJdEXsycYDprI_Hhf-yXSbDCGV_DH_4Ny4ZxXmTUQhQm0TAt52tYW4xvXRtERT9OywU6LqN4gWZZtFyS_dcXPpuMhsPBZAqL-fGbv-3XqK69f8zi4OUbJQ4aBRNXpE0hzV1_i5glxLauvkXSFpLCwbfIOZJx69gd0V2TeWlwhTNuAXA_nAXVZN5F_95gcnl8f3Tq0UmefV9Tqy3EY-Z6-up_PzxVLUZWRh26oNphFOMmweoEZoVAGPHdNK2KZsWu76ZsV5Slqd9N1anOW7H-Qe1dd_SyIgr9oICjtIzgENywN70Jm-K7XQE6gZLLyMEiOY6-i9b-EsCMysO22GJ2U-q9co4zOJuQST28iVNqPyUU7rnTS28wPr34lJyfP_5AdlzRG94b1CxzMjg9owftT0TwBMdr1Cdlg64rhzyBwUw1je03Oed00J8MZlMW3s_QFAcZVtIg-WNi_LB-LSMnv1PcFOLU4_lhBUsoyPg6qGILlWWQNX6Tp0njCtfzowyD3XioGHeC87TMwL-KT8YXHjPON59Vxcfpor4ikOPW-c--kjZOs6KLrFarRYeOYZ5FDWMYof74fheZTmvdcFqttUppCspqqTtLk2XqHaOfoJ99MlM1LKGhVDko39EGo1FS4GW2Wx5B0xaatVo3TvNimeHpz09VeUfOpNQ6kI0KjDy_8OekUVH02kLvvDebQsBl17w-MRvZpmnecYSpUj9dr8tElPm6w4jAZf_i7IwVxDf7NKorovLTT8_7ojua4N-WpIOBchsz5xHjN6_9OFqARykittwMo2TRi-Ndxh6nJGVwcE0cQRWpbZsQ0MDEshf3UzNI15sYYuuu_DXlOUjZ8nQw-XjUH_BD_M-tWHVV04_7LECht6oHqCpmimTAg059z0IMmqZtiKkiLJagSxKxpArwRunbavCoMm3hQZpxcxoodxhnlECc5jm4OgmjZZntC47R-XAymJL4OP9oNBTmGDyCzJ34MeoFtEDX1jE9ZeZ4Tr6iPiYVgsQRCwR_EzXyPG4EgO-1J8zI0sd31QUWpEFXmozBL3h-_fIr0fiSJnibzZvrvGnZTbfZsZqGZTaTaNOMUpWDe--VbGnRJ3i-StOrO0wnDXBLgAHtYHLeOxXL25WvmQy6wPFABAlPPLCTelnvzXrHvSkP2ldfkBImMkYtzeloTwra3QJI05tKslR76Yvz0exiIvzw4vdV0Xo57Z3OTsiR_cs_WEH142IFJRUHV2qun87Oerzj_hdd39pPwK_g06CWYHbX-RFc7kgEJEwyl9c4cUljAGnKKcCaexU0VMBUAUsFbBVwqisDSgpDQy4AkwOC-sTigKA-sTkgqE8cDtSogZLCniHGjNkzxZgRe5YYM17PFmNG69VYPUbam_ChWR9a9aFdHzq1oWgCKUiaKgaQbxTivc9e1NyLWntRuzqdfEcaBwbxeQRqVlFToHYVtQRqVVFboM7uVO3qGsiYvpA1cB_e276QcsrKt3LKC8nHdkVqkIRMAZkSsgRkScgWkC0hR0COslxSM6rzkunoCzj8ErEUBJJ6DYAvFCDpeAcxq_RkzOalCU_ZmExwylYUXLEQS0KSXwQDzTdqM1DcxDLdBbGf5x4O0TIqyO8ECK5Dcfe90MJO6Ohwk0mvcPe9ztwIfZMPGw-jRbHqmptHCgX5TajCgV3sh23JYYWOMXfqHNYOR0Bu_uzay1ms0AwXksU46rQXB1fCLlOCwQidEEuGlum6C-MQQ8bvccIeAbZxIDkC03Cd-SGOKzeXpggd7G5N4brYCg6pb-CqIPRbYARju4VW-8g5qE-6n9tM0OnMF4f0xcVVmMAIXXwkORzHnZvhIY6Ity6cIgSK7TbCI981nUMUWPQMggPP8XYrC8sMDy9jLSv3_vh2sWn7_i0sFS5S7nSocPCx4GPrpHTxk1MXo9VXnojqOyhrOpQy-FjwsXVSprZRX5X0DN0zdc_SPVuH5MV_IagIQOnJaj9IMJjkbZ0XBf7f5P8tXaR6CM6qDkkkOslB5GGRh00ejk6TJAnFqrTM53olg5N4qwqRLKqTNE0eFnnY5OGQR1tGV01jeqpD0tRJAtNpluTxUxOiSVOX6VAGSN0EJB3qPAFW_K_p2jKLFlq3yEqsa2ucgY9gqD0m6g-0YoXXcPPswteFn0Hv-yB5AjobP_llmq6FWpaWy5XWDf04h1G5Ifc7L_KhcVxLNIMeDmf9tEwKreu4lEPrPtYeaV3TsZstt91xLMsyO3Cnt3XtRutCe-6aJLM4hnvUMlqdJ7r2Ozprq-m22obRcY_clt3uHJnOk_8DTtWHgw))

🔗 **[View Interactive Diagram](https://mermaid.live/edit#pako:eNqNWFuP28YV_isDBnkqpYg3iSsUAbSiolW9F1WSk6Z1saCoocQuRaq8rL01DCRAnoqkdmwDblMUbosiNfLQPuShAfpv8gfqn9AzV5Ej7coLiKv5eM43M-ecOeeMHmtBusBaVwvj9GGw8rMCzbwHCYK_999HHr7GcbpZ46RA45WfY_YG4F890N6-_vrNj5999fb18_8CkvtZlsZxik7TwI8faL9GjcaHaBgVVPLlF-QrGpf5Cvlo7UcJSDAyORkInJRzNMGbNI-KNItwjqZFVgZFmfGJ83K-zPzNCg1Hs5P7x5cXkyGlf_p3lOC8aKyjIEtznF1HAc4bCY7lLORveGJQ6RefoyCOYE-NpV_gh_7NT-fZBx--ff3lM9Qbj9CQgYqqKVT9slg11jnXeQk6AABZFPhFlCaKmiXUNv4NMWPeEJrPv0djjik6ttBJswXOtnP9-Tm6IIgq78g5snQB5sq3Ki--RWMOSiWcLKqWlzY9643OLyeD8QUz6V_RGbhp6w7VIJdEXsycYDprI_Hhf-yXSbDCGV_DH_4Ny4ZxXmTUQhQm0TAt52tYW4xvXRtERT9OywU6LqN4gWZZtFyS_dcXPpuMhsPBZAqL-fGbv-3XqK69f8zi4OUbJQ4aBRNXpE0hzV1_i5glxLauvkXSFpLCwbfIOZJx69gd0V2TeWlwhTNuAXA_nAXVZN5F_95gcnl8f3Tq0UmefV9Tqy3EY-Z6-up_PzxVLUZWRh26oNphFOMmweoEZoVAGPHdNK2KZsWu76ZsV5Slqd9N1anOW7H-Qe1dd_SyIgr9oICjtIzgENywN70Jm-K7XQE6gZLLyMEiOY6-i9b-EsCMysO22GJ2U-q9co4zOJuQST28iVNqPyUU7rnTS28wPr34lJyfP_5AdlzRG94b1CxzMjg9owftT0TwBMdr1Cdlg64rhzyBwUw1je03Oed00J8MZlMW3s_QFAcZVtIg-WNi_LB-LSMnv1PcFOLU4_lhBUsoyPg6qGILlWWQNX6Tp0njCtfzowyD3XioGHeC87TMwL-KT8YXHjPON59Vxcfpor4ikOPW-c--kjZOs6KLrFarRYeOYZ5FDWMYof74fheZTmvdcFqttUppCspqqTtLk2XqHaOfoJ99MlM1LKGhVDko39EGo1FS4GW2Wx5B0xaatVo3TvNimeHpz09VeUfOpNQ6kI0KjDy_8OekUVH02kLvvDebQsBl17w-MRvZpmnecYSpUj9dr8tElPm6w4jAZf_i7IwVxDf7NKorovLTT8_7ojua4N-WpIOBchsz5xHjN6_9OFqARykittwMo2TRi-Ndxh6nJGVwcE0cQRWpbZsQ0MDEshf3UzNI15sYYuuu_DXlOUjZ8nQw-XjUH_BD_M-tWHVV04_7LECht6oHqCpmimTAg059z0IMmqZtiKkiLJagSxKxpArwRunbavCoMm3hQZpxcxoodxhnlECc5jm4OgmjZZntC47R-XAymJL4OP9oNBTmGDyCzJ34MeoFtEDX1jE9ZeZ4Tr6iPiYVgsQRCwR_EzXyPG4EgO-1J8zI0sd31QUWpEFXmozBL3h-_fIr0fiSJnibzZvrvGnZTbfZsZqGZTaTaNOMUpWDe--VbGnRJ3i-StOrO0wnDXBLgAHtYHLeOxXL25WvmQy6wPFABAlPPLCTelnvzXrHvSkP2ldfkBImMkYtzeloTwra3QJI05tKslR76Yvz0exiIvzw4vdV0Xo57Z3OTsiR_cs_WEH142IFJRUHV2qun87Oerzj_hdd39pPwK_g06CWYHbX-RFc7kgEJEwyl9c4cUljAGnKKcCaexU0VMBUAUsFbBVwqisDSgpDQy4AkwOC-sTigKA-sTkgqE8cDtSogZLCniHGjNkzxZgRe5YYM17PFmNG69VYPUbam_ChWR9a9aFdHzq1oWgCKUiaKgaQbxTivc9e1NyLWntRuzqdfEcaBwbxeQRqVlFToHYVtQRqVVFboM7uVO3qGsiYvpA1cB_e276QcsrKt3LKC8nHdkVqkIRMAZkSsgRkScgWkC0hR0COslxSM6rzkunoCzj8ErEUBJJ6DYAvFCDpeAcxq_RkzOalCU_ZmExwylYUXLEQS0KSXwQDzTdqM1DcxDLdBbGf5x4O0TIqyO8ECK5Dcfe90MJO6Ohwk0mvcPe9ztwIfZMPGw-jRbHqmptHCgX5TajCgV3sh23JYYWOMXfqHNYOR0Bu_uzay1ms0AwXksU46rQXB1fCLlOCwQidEEuGlum6C-MQQ8bvccIeAbZxIDkC03Cd-SGOKzeXpggd7G5N4brYCg6pb-CqIPRbYARju4VW-8g5qE-6n9tM0OnMF4f0xcVVmMAIXXwkORzHnZvhIY6Ity6cIgSK7TbCI981nUMUWPQMggPP8XYrC8sMDy9jLSv3_vh2sWn7_i0sFS5S7nSocPCx4GPrpHTxk1MXo9VXnojqOyhrOpQy-FjwsXVSprZRX5X0DN0zdc_SPVuH5MV_IagIQOnJaj9IMJjkbZ0XBf7f5P8tXaR6CM6qDkkkOslB5GGRh00ejk6TJAnFqrTM53olg5N4qwqRLKqTNE0eFnnY5OGQR1tGV01jeqpD0tRJAtNpluTxUxOiSVOX6VAGSN0EJB3qPAFW_K_p2jKLFlq3yEqsa2ucgY9gqD0m6g-0YoXXcPPswteFn0Hv-yB5AjobP_llmq6FWpaWy5XWDf04h1G5Ifc7L_KhcVxLNIMeDmf9tEwKreu4lEPrPtYeaV3TsZstt91xLMsyO3Cnt3XtRutCe-6aJLM4hnvUMlqdJ7r2Ozprq-m22obRcY_clt3uHJnOk_8DTtWHgw)**

### 📋 Architecture Overview
- **5 Microservices** with independent deployment
- **NATS** for async communication  
- **Google Cloud** CI/CD pipeline
- **Kubernetes** orchestration
- **Zero-downtime** deployments

This main repository contains the orchestration configuration for all store microservices. Each microservice is stored in a separate repository within the organization `nest-microservices-nel` and is included as a git submodule:

- **client-gateway**: Main gateway that exposes REST APIs
- **products-ms**: Product management microservice
- **orders-ms**: Order management microservice
- **payments-s**: Payment microservice (integrated with Stripe)
- **auth-mss**: Authentication and authorization microservice

## Installation and Configuration

### 1. Clone the Repository

```bash
git clone https://github.com/nelsin-06/nets-ms-nats-launcher.git
cd nets-ms-nats-launcher
```


### 2. Download Submodules

```bash
git submodule update --init --recursive
```


### 3. Configure Environment Variables

Crea un archivo `.env` basado en `.env.template`:

```bash
cp .env.template .env
```


**Required variables:**
- `PORT_CLIENT_GATEWAY_HOST`: Gateway port (default: 8080)
- `DATABASE_MONGO_URL`: MongoDB connection URL for auth-ms
- `STRIPE_SECRET`: Stripe secret key
- `STRIPE_SIGNING_WEBHOOK_ENDPOINT`: Stripe webhook endpoint
- `JWT_SECRET`: Secret for JWT tokens

## Project Execution (use the production option if you want to run the project using the Docker image from the cloud)


### Production

```bash
docker compose -f docker-compose.prod.yml up --build
```

### Development with Docker Compose

```bash
docker compose up --build
```

**Nota:** En desarrollo, algunos microservicios están comentados en el docker-compose.yml para facilitar el desarrollo individual.

## Kubernetes Configuration

El proyecto incluye configuraciones completas para despliegue en Kubernetes usando Helm charts ubicadas en `k8s/store-ms/`.

### K8s Structure

```
k8s/store-ms/
├── Chart.yaml              # Helm chart configuration
├── values.yaml             # Default values
└── templates/              # Kubernetes manifests
    ├── auth-ms/
    ├── client-gateway/
    ├── orders-ms/
    ├── payments-ms/
    ├── products-ms/
    ├── nats/
    └── ingress/
```

### Deployment on Kubernetes

1. **Create required secrets:**
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

3. **Deploy with Helm:**
```bash
# Initial installation
helm install store-ms k8s/store-ms/

# Updates
helm upgrade store-ms k8s/store-ms/
```

### K8s Configuration Features

- **Ingress with SSL**: Automatic SSL certificates for configured domains
- **Persistent Volumes**: For products-ms data persistence (SQLite)
- **Resource Limits**: CPU and memory limit configuration
- **Health Checks**: Configured liveness and readiness probes
- **Secrets Management**: Sensitive variables handled as Kubernetes secrets

## Useful Commands

### Git Submodules
```bash
# Actualizar todos los submódulos a la última versión
git submodule update --remote

# Actualizar un submódulo específico
git submodule update --remote <submodule-name>
```

### Kubernetes
```bash
# Check pod status
kubectl get pods

# View logs of a pod
kubectl logs <pod-name>

# View services
kubectl get services

# View ingress
kubectl get ingress
```

## Important

When working with submodules, always **update and push the submodule first** and **then the main repository**. If done in reverse order, submodule references will be lost.

## Access URLs

- **Development**: http://localhost:8080
- **Production K8s**: Configured via Ingress (see ingress files for specific URLs)
