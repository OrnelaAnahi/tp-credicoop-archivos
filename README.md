# 🏗️ Trabajo Práctico Final - Curso de Infraestructura Tecnológica

Repositorio con los archivos utilizados en el Trabajo Práctico Final del curso de **Infraestructura Tecnológica**, dictado por la **Universidad Tecnológica Nacional (UTN)** en conjunto con el **Banco Credicoop** durante el año 2024.

## 📚 Descripción del Proyecto

El objetivo de este trabajo fue aplicar los conocimientos adquiridos a lo largo del curso, desarrollando un entorno completo de integración y despliegue continuo (CI/CD), junto con tareas automatizadas de infraestructura.

El proyecto se divide en dos grandes partes:

1. **Desarrollo y CI/CD**  
   - Despliegue de una aplicación web (Appx-API) conectada a una base de datos.
   - Uso de **Jenkins** para automatizar:
     - Pull de cambios desde un repositorio Git.
     - Ejecución de pruebas.
     - Análisis de calidad de código con **SonarQube**.
     - Despliegue automático en un clúster local de **Minikube**.

2. **Automatización de Infraestructura con Ansible**  
   - Instalación y configuración de una "BoxedApp" (aplicación web con base de datos, distinta de la Appx-API).
   - Automatización de tareas como backups o modificaciones.
   - Escalado o desescalado manual de la Appx-API desde Ansible.

## 🧰 Herramientas Utilizadas

- **Docker & Docker Compose**
- **Minikube & Kubernetes**
- **Jenkins**
- **SonarQube**
- **Ansible**
- **Git & GitHub**
- **Aplicaciones BoxedApp (como Redmine, Moodle, MediaWiki, etc.)**
