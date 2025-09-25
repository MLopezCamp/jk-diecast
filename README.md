# 🏎️ JK-Diecast – Taller de Jenkins + Docker

Este proyecto es un taller práctico para demostrar **integración de Jenkins con Docker**, utilizando **Docker-in-Docker (DinD)** para construir y desplegar una aplicación web sencilla (un `index.html` servido por Nginx).

---

## 📌 Arquitectura

- **Jenkins**  
  Corre en un contenedor, con acceso al daemon de DinD, y ejecuta el pipeline.
- **DinD (Docker-in-Docker)**  
  Contenedor que levanta un daemon de Docker independiente donde Jenkins construye imágenes y ejecuta los contenedores de la aplicación.
- **App Web (jk-diecast)**  
  Una página estática `index.html` servida con Nginx. Se despliega automáticamente desde Jenkins.

---

## 📂 Estructura del proyecto

```
.
├── Dockerfile.jenkins   # Imagen custom de Jenkins con Docker CLI instalado
├── Dockerfile           # Imagen de la app web (usa nginx:alpine)
├── docker-compose.yml   # Orquesta Jenkins y DinD
├── index.html           # Página estática a mostrar
├── Jenkinsfile          # Pipeline de CI/CD
└── README.md            # Este archivo
```

---

## ⚙️ Requisitos previos

- Docker Desktop o Docker Engine ≥ 20.x
- Docker Compose v2
- Git

---

## 🚀 Pasos de instalación

1. **Clonar el repositorio**  
   ```bash
   git clone https://github.com/MLopezCamp/jk-diecast.git
   cd jk-diecast
   ```

2. **Levantar Jenkins + DinD**  
   ```bash
   docker compose up -d --build
   ```

3. **Acceder a Jenkins**  
   - URL: [http://localhost:8083](http://localhost:8083)  
   - Usuario inicial: configurado al instalar (ejecutar `docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword` para obtener la clave).  

4. **Configurar Jenkins**  
   - Instalar plugins recomendados.  
   - Crear un nuevo pipeline SCM conectado a este repositorio.
   - Dar a construir. 

---

## 🔄 Pipeline (Jenkinsfile)

El pipeline consta de los siguientes stages:

1. **Checkout** → Clona el repositorio desde GitHub.  
2. **Docker Login** → Inicia sesión en Docker Hub (evita límites de pulls).  
3. **Build Docker Image** → Construye la imagen `jk-diecast:latest` desde el `Dockerfile`.  
4. **Run Container** → Elimina el contenedor previo (si existe) y lanza uno nuevo en el DinD.  

---

## 🌐 Acceso a la aplicación

Una vez ejecutado el pipeline:

- Jenkins construirá y correrá la imagen dentro de DinD.
- El contenedor de la app expone el puerto **8082**, que se mapea al host.
- Abre en el navegador:

👉 [http://localhost:8082](http://localhost:8082)

Deberías ver el contenido de `index.html`.

---

## 📖 Notas

- Se utiliza **Docker-in-Docker** para que Jenkins gestione un daemon Docker aislado.  
- El puerto `8083` es para Jenkins y el `8082` para la aplicación.
- ña carpeta jenkinshome se crea automaticamente para la persistencia de jenkins y el uso de DinD.

---

## 👨‍💻 Autor

Mauricio López Campiño  
Proyecto académico para prácticas con **Jenkins, Docker y CI/CD**.
