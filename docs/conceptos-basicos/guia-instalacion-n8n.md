# Instalación de n8n

Este repositorio recopila diferentes formas de instalar y desplegar **n8n**, una herramienta de automatización de flujos de trabajo.

Aquí encontrarás un panorama general de las opciones disponibles, con sus ventajas y casos de uso más comunes.

![alt text](./n8n-instalacion.png)
---

## Opciones de instalación

### 1. **n8n Cloud**

* Servicio oficial gestionado en [n8n.io](https://n8n.io)
* No requiere instalación ni mantenimiento.
* Ideal para quienes buscan simplicidad, soporte oficial y alta disponibilidad.

📄 **Guía:** [Próximamente](docs/n8n-cloud.md)

---

### 2. **Instalación Local**

Puedes ejecutar n8n directamente en tu máquina personal para fines de pruebas y aprendizaje:

* **npm** → Instalación usando Node.js y NPM
* **Docker** → Despliegue mediante contenedores, recomendado por su portabilidad

📄 **Guías:**

* [Instalación con npm](docs/n8n-npm.md)
* [Instalación con Docker](docs/n8n-docker.md)

---

### 3. **Alojado en la Nube (Hosting)**

Existen dos enfoques principales para correr n8n en la nube:

#### a) Plataforma como Servicio (PaaS)

Soluciones que abstraen la infraestructura y simplifican el despliegue:

* Railway
* Heroku
* Render
* Vercel
* Cloudflare
* Netlify

📄 **Ejemplo de guía completa:**

* [Instalación en Render con Supabase](docs/n8n-render-supabase.md)

---

#### b) Infraestructura como Servicio (IaaS)

Proveedores de máquinas virtuales (VPS) y recursos escalables para un control total:

* AWS
* Google Cloud
* Microsoft Azure
* DigitalOcean
* IBM Cloud
* Oracle Cloud (OCI)
* Hostinger VPS

📄 **Guías sugeridas:**

* [Instalación en AWS](docs/n8n-aws.md)
* [Instalación en DigitalOcean](docs/n8n-digitalocean.md)
* [Instalación en Hostinger VPS](docs/n8n-hostinger.md)

---

## Recomendaciones según escenario

* 🚀 **Inicio rápido sin complicaciones** → n8n Cloud
* 🧪 **Pruebas locales** → npm o Docker
* ⚡ **Producción simplificada** → Render, Railway u otro PaaS
* 🛠️ **Producción con máximo control** → VPS o IaaS (ej. AWS, DigitalOcean)

---

## Índice de documentos

* `docs/n8n-cloud.md` → Guía para usar n8n Cloud
* `docs/n8n-npm.md` → Instalación local con npm
* `docs/n8n-docker.md` → Instalación local con Docker
* `docs/n8n-render-supabase.md` → Render + Supabase (plan gratuito)
* `docs/n8n-aws.md` → Instalación en AWS
* `docs/n8n-digitalocean.md` → Instalación en DigitalOcean
* `docs/n8n-hostinger.md` → Instalación en VPS Hostinger

---

✍️ Autor: **Profesor Ronald Cuello**
📍 Colombia – 2025

---

