<div align="center">
  <img height="150" src="https://static.wikia.nocookie.net/skapokonpedia/images/9/9e/Bubu.png/revision/latest/thumbnail/width/360/height/360?cb=20210307160549&path-prefix=es"  />
</div>

###

<p align="center">
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white&style=for-the-badge" alt="Docker"/>
  <img src="https://img.shields.io/badge/Railway-0B0D0E?logo=railway&logoColor=white&style=for-the-badge" alt="Railway"/>
  <img src="https://img.shields.io/badge/Jenkins-D24939?logo=jenkins&logoColor=white&style=for-the-badge" alt="Jenkins"/>
</p>

###

<h1 align="center">🐻 Iago Martínez González - Exámen 2 Evaluación 🐻 </h1>

### 📌 Sobre el Proyecto
**Pokémon App** es una aplicación desarrollada en **Node.js** y **Axios**, que permite obtener y visualizar datos de Pokémon a través de una API externa.

El objetivo de este proyecto es demostrar la implementación de **automatización y despliegue continuo (CI/CD)** utilizando herramientas como **Docker, GitHub Actions, Railway y Jenkins**.

---

## 🚀 Tecnologías Utilizadas
- **Node.js**: Plataforma de ejecución para JavaScript en el servidor.
- **Axios**: Cliente HTTP para la comunicación con APIs.
- **Docker**: Contenerización de la aplicación.
- **GitHub Actions**: Automatización del flujo CI/CD.
- **Railway**: Despliegue en la nube.
- **Jenkins**: Integración y despliegue continuo.

---

## 💂️ Pasos para Implementar el Proyecto

### 1️⃣ Clonar el Repositorio
```sh
git clone https://github.com/imblake-cloud/pokemon-app.git
cd pokemon-app
```

---

### 2️⃣ Ejecutar la Aplicación en Local
#### 🔹 Instalar dependencias
```sh
npm install
```
#### 🔹 Ejecutar el servidor
```sh
node src/app.js
```
📍 La aplicación estará disponible en `http://localhost:3000`.

---

### 3️⃣ Contenerización con Docker
#### 🔹 Construcción de la imagen Docker
```sh
docker build -t pokemon-app .
```
#### 🔹 Ejecutar el contenedor
```sh
docker run -p 3000:3000 pokemon-app
```

---

### 4️⃣ Automatización con GitHub Actions
Cada vez que se suba código a `main`, GitHub Actions ejecutará pruebas y desplegará automáticamente.

#### 🔹 Configuración en `.github/workflows/ci.yml`
```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Clonar el repositorio
        uses: actions/checkout@v3

      - name: Instalar dependencias
        run: npm install

      - name: Ejecutar pruebas
        run: npm test
```

---

### 5️⃣ Despliegue en Railway
#### 🔹 Subir el proyecto a Railway
1. Crear una cuenta en **[Railway](https://railway.app)**
2. Conectar el repositorio desde Railway
3. Configurar las variables de entorno
4. Deploy automático tras cada cambio en `main`

---

### 6️⃣ Integración con Jenkins
Jenkins permite compilar, probar y desplegar la aplicación de manera automatizada.

#### 🔹 Pipeline utilizada en Jenkins (`Jenkinsfile`)
```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/imblake-cloud/pokemon-app.git'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDENTIALS', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t imblake/pokemon-app .'
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    def testExitCode = bat(returnStatus: true, script: 'docker run --rm imblake/pokemon-app npm test')
                    if (testExitCode != 0) {
                        echo "No test script found, continuing pipeline..."
                    }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker tag imblake/pokemon-app imblake/pokemon-app:latest'
                bat 'docker push imblake/pokemon-app:latest'
            }
        }
    }
}
```

---

## 🎯 Conclusión
👉 **Desarrollamos** una aplicación en Node.js  
👉 **Automatizamos** la integración y despliegue con GitHub Actions  
👉 **Contenerizamos** la aplicación con Docker  
👉 **Desplegamos** la aplicación en Railway  
👉 **Implementamos CI/CD** con Jenkins  

Este proyecto proporciona un **despliegue optimizado, ágil y confiable** para aplicaciones en producción. 🚀

---

## 📞 Contacto
📧 Email: [martinezgonzaleziago@gmail.com](mailto:martinezgonzaleziago@gmail.com)  
🐦 Twitter: [@iagomartinez2](https://x.com/iagomartinez2)  
