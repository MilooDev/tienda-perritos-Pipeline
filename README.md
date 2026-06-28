# 🐶 Innovatech: Tienda de Alimentos para Perritos (Arquitectura Cloud)

## 📌 Descripción del Proyecto
Este repositorio contiene la infraestructura como código, la contenedorización y los flujos automatizados para la aplicación de gestión de inventario "Innovatech". El proyecto ha sido modernizado mediante una arquitectura de microservicios, separando las capas de Frontend (SPA/Nginx), Backend (Node.js/Express) y Base de Datos (MySQL).

## 🚀 Arquitectura y Tecnologías
* **Orquestación:** AWS ECS Fargate (Serverless)
* **Contenedores:** Docker & Amazon Elastic Container Registry (ECR)
* **CI/CD:** GitHub Actions
* **Redes:** AWS VPC, Application Load Balancer, Security Groups.

## ⚙️ Funcionamiento del Pipeline (CI/CD)
El despliegue está completamente automatizado. Al realizar un `push` a la rama `main`, el flujo `deploy.yml` ejecuta los siguientes pasos:
1. Autenticación segura mediante AWS Credentials (GitHub Secrets).
2. Construcción de imágenes Docker (Frontend y Backend).
3. Etiquetado y Push hacia Amazon ECR.
4. Ejecución del comando `aws ecs update-service` para desplegar las nuevas versiones sin tiempo de inactividad (Zero Downtime).

## 🛠️ Variables de Entorno (Secrets)
Para ejecutar este proyecto, se requiere configurar los siguientes secretos en el repositorio:
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_SESSION_TOKEN`
* `AWS_REGION`
* `ECS_CLUSTER`
* `ECS_FRONTEND_SERVICE`
* `ECS_BACKEND_SERVICE`

## 📖 Cómo utilizar (Despliegue Local)
Si deseas levantar la infraestructura de manera local para pruebas:
1. Clona el repositorio: `git clone <url-del-repo>`
2. Navega a la carpeta principal y levanta los servicios mediante Docker Compose (si aplica) o construye las imágenes manualmente:
   ```bash
   docker build -t frontend-app ./frontend
   docker build -t backend-api ./backend
