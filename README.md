
---

# **SIT323/SIT737 - Cloud Native Application Development**
## **5.1P: Containerisation of a Simple Web Application Using Docker**

---

### **Overview**
This project demonstrates the containerization of a simple web application using Docker. The process involves creating a `Dockerfile` to define the application's environment, building a Docker image, and deploying the application using Docker Compose. The application is then tested locally to ensure functionality.

---

### **Tools Used**
To complete this task, the following tools were used:
- **Git**: [https://github.com](https://github.com)
- **Visual Studio Code**: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- **Node.js**: [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
- **Docker**: [https://www.docker.com/](https://www.docker.com/)

---

### **Repository Structure**
The repository contains the following files:
- **Application Source Code**: The main application files.
- **Dockerfile**: Defines the steps to build the Docker image.
- **docker-compose.yml**: Configures the Docker Compose environment.
- **README.md**: This documentation file.

---

### **Steps to Dockerize the Application**

#### **1. Install Docker**
- Download and install Docker Desktop from the official website: [https://www.docker.com/](https://www.docker.com/).
- Ensure Docker is running on your machine after installation.
- Verify the installation by running:
  ```bash
  docker --version
  ```

#### **2. Clone the Application**
- Clone the repository containing the application code:
  ```bash
  git clone https://github.com/AnudhaUthsala/sit323-2025-prac5p.git
  cd sit323-2025-prac5p
  ```

#### **3. Create the Dockerfile**
- Add a `Dockerfile` to the root directory with the following content:
  ```dockerfile
  
  FROM node:lts-alpine
  
  ENV NODE_ENV=production
  
  WORKDIR /usr/src/app
  
  COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
  
  RUN npm install --production --silent && mv node_modules ../
  
  COPY . .
  
  EXPOSE 3000
  
  RUN chown -R node /usr/src/app
  
  USER node
  
  CMD ["npm", "start"]
  

  ```

#### **4. Build the Docker Image**
- Build the Docker image using the following command:
  ```bash
  docker build -t sit323-2025-prac5p .
  ```
- Verify that the image was created successfully:
  ```bash
  docker images
  ```

#### **5. Create the Docker Compose File**
- Add a `docker-compose.yml` file with the following content:
  ```yaml
  version: '3.4'
  services:
    calculatormicroservice:
      image: calculatormicroservice
      build:
        context: .
        dockerfile: ./Dockerfile
      environment:
        NODE_ENV: production
      ports:
        - 3000:3000```

#### **6. Start the Docker Compose Environment**
- Start the container using Docker Compose:
  ```bash
  docker-compose up
  ```
- Open a browser and navigate to `http://localhost:3000` to verify the application is running.

#### **7. Test the Application**
- Open a browser and navigate to `http://localhost:3000`.
- Ensure the application is functioning as expected.

#### **8. Push the Docker Image to a Registry**
- Log in to Docker Hub:
  ```bash
  docker login
  ```
- Tag your Docker image:
  ```bash
  docker tag sit323-2025-prac5p AnudhaUthsala/sit323-2025-prac5p:latest
  ```
- Push the image to Docker Hub:
  ```bash
  docker push AnudhaUthsala/sit323-2025-prac5p:latest
  ```



