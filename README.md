# Despliegue Automatizado de Infraestructura en AWS mediante GitHub Actions

Este proyecto corresponde al examen final de la asignatura **Arquitectura Orientada a Servicios** (Programa de Ingeniería de Sistemas). Su desarrollo implementa prácticas de Integración y Despliegue Continuo (CI/CD) combinadas con Infraestructura como Código (IaC).

**Estudiante:** Keiner Josué Barbosa Calderon  
**Código:** 0192502  

---

## 🎯 Objetivo del Proyecto
El objetivo principal es diseñar, versionar, desplegar y eliminar de forma completamente automatizada una instancia virtual en la nube de AWS. Para esto se integra un flujo de trabajo basado en Git Flow y GitHub Actions, garantizando un entorno controlado, colaborativo y de rápida iteración.

---

## 🛠️ Tecnologías Utilizadas
* **AWS (Amazon Web Services):** Proveedor de nube para alojar la infraestructura.
* **AWS CloudFormation:** Herramienta de Infraestructura como Código (IaC) utilizada para definir los recursos mediante plantillas en formato YAML.
* **GitHub Actions:** Plataforma de CI/CD para automatizar los flujos de validación, despliegue y destrucción.
* **Git / GitHub:** Control de versiones bajo la metodología Git Flow.
* **Linux (Amazon Linux 2/2023):** Sistema operativo base de la instancia EC2.
* **Apache (httpd), HTML, CSS, JS:** Servidor web y tecnologías frontend para exponer la página web solicitada.

---

## 🚀 Funcionalidad de Deploy (`deploy.yml`)
El flujo de trabajo de despliegue automatizado realiza las siguientes acciones al activarse:
1. **Validación:** Analiza la sintaxis de la plantilla de CloudFormation (`ec2.yaml`) para asegurar que no contenga errores de estructura.
2. **Autenticación:** Se conecta de forma segura a AWS utilizando las credenciales `AWS_ACCESS_KEY_ID` y `AWS_SECRET_ACCESS_KEY` almacenadas en los Secrets del repositorio.
3. **Aprovisionamiento:** Crea o actualiza el Stack en CloudFormation, aprovisionando la instancia EC2 y el Security Group asociado de manera automática.

---

## 🗑️ Funcionalidad de Destroy (`destroy.yml`)
El flujo de trabajo de destrucción está diseñado para la limpieza y optimización de costos en el entorno cloud:
* Se ejecuta bajo demanda para **eliminar por completo el Stack** de CloudFormation.
* Garantiza la remoción ordenada de todos los recursos vinculados (la instancia EC2, configuraciones de red y el Security Group), dejando el entorno de AWS limpio y sin cargos residuales.

---

## 🖥️ Objetivo del Template EC2 Creado (`ec2.yaml`)
La plantilla de CloudFormation tiene como propósito definir el estado deseado de la infraestructura requerida:
* **Instancia EC2:** Levanta un servidor virtual basado en Amazon Linux.
* **Security Group:** Habilita de forma específica el **Puerto 80 (HTTP)** para permitir que el tráfico web público acceda al servidor.
* **User Data:** Script de inicialización automatizada que instala el servidor web Apache, configura los servicios al arrancar el sistema y genera un archivo `index.html` dinámico con los datos de **Keiner Josué Barbosa Calderon (Código: 0192502)** y el texto identificador del Examen Final.