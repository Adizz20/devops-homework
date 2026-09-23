# Docker Fundamental — Homework

**Name:** Aditya Vikram Singh
**Roll No.:** 24bcs10429

## Task: Hello World Applications

## Overview

Four different "Hello World" applications were containerized with Docker: Node.js, Python, Java, and Apache HTTP Server. Each app has its own folder and Dockerfile; each image was built and run, and the result was verified through a browser.

---

## 1. Node.js Application

### Objective
Create a simple Node.js web application, containerize it with Docker, and access it via a browser.

### Application Code (`server.js`)
```javascript
const http = require("http");

const server = http.createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/html" });

    res.end(`
        <h1>Hello World from Node.js + Docker!</h1>
        <p><strong>Name:</strong> Aditya Vikram Singh</p>
        <p><strong>Roll No:</strong> 24bcs10429</p>
    `);
});

server.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

### Dockerfile
```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package.json .
COPY server.js .

EXPOSE 3000

CMD ["npm", "start"]
```

### Build & Run
```bash
docker build -t node .
docker run -d --name node-container -p 3000:3000 node
```
Accessed at: `http://localhost:3000`

### Output
![Node.js Hello World output](<images/Screenshot (82).png>)

### Images

![Node.js Hello World output](<images/Screenshot (82).png>)

The Node.js application successfully displayed the Hello World webpage.

---

## 2. Python Application

### Objective
Create a simple Python (Flask) web application, containerize it with Docker, and access it via a browser.

### Application Code (`app.py`)
```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return """
    <h1>Hello World from Python + Docker!</h1>
    <p><strong>Name:</strong> Aditya Vikram Singh</p>
    <p><strong>Roll No:</strong> 24bcs10429</p>
    """

app.run(host="0.0.0.0", port=5000)
```

### Requirements (`requirements.txt`)
```
flask
```

### Dockerfile
```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

### Build & Run
```bash
docker build -t hello-python .
docker run -d --name hello-python-container -p 5001:5000 hello-python
```
Port `5001` was used on the host because port `5000` was already occupied. Accessed at: `http://localhost:5001`

### Output
![Python Hello World output](<images/Screenshot (85).png>)

### Images

![Python Hello World output](<images/Screenshot (85).png>)

The Python application successfully displayed the Hello World webpage.

---

## 3. Java Application

### Objective
Create a simple Java web application, containerize it with Docker, and access it via a browser.

### Application Code (`Main.java`)
```java
import com.sun.net.httpserver.HttpServer;
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;

public class Main {
    public static void main(String[] args) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(8080), 0);

        server.createContext("/", exchange -> {
            String response = """
                <h1>Hello World from Java + Docker!</h1>
                <p><strong>Name:</strong> Aditya Vikram Singh</p>
                <p><strong>Roll No:</strong> 24bcs10429</p>
                """;

            exchange.sendResponseHeaders(200, response.getBytes().length);

            try (OutputStream os = exchange.getResponseBody()) {
                os.write(response.getBytes());
            }
        });

        server.start();

        System.out.println("Java server running on port 8080");
    }
}
```

### Dockerfile
```dockerfile
FROM eclipse-temurin:21-jdk-alpine

WORKDIR /app

COPY Main.java .

RUN javac Main.java

EXPOSE 8080

CMD ["java", "Main"]
```

### Build & Run
```bash
docker build -t hello-java .
docker run -d --name hello-java-container -p 8080:8080 hello-java
```
Accessed at: `http://localhost:8080`

### Output
![Java Hello World output](<images/Screenshot (84).png>)

### Images

![Java Hello World output](<images/Screenshot (84).png>)

The Java application successfully displayed the Hello World webpage.

---

## 4. Apache Web Server

### Objective
Create a simple webpage and serve it using the Apache HTTP Server inside a Docker container.

### HTML Application (`index.html`)
```html
<!DOCTYPE html>
<html>
<head>
    <title>Apache Docker App</title>
</head>
<body>
    <h1>Hello World from Apache + Docker!</h1>
    <p><strong>Name:</strong> Aditya Vikram Singh</p>
    <p><strong>Roll No:</strong> 24bcs10429</p>
</body>
</html>
```

### Dockerfile
```dockerfile
FROM httpd:2.4-alpine

COPY index.html /usr/local/apache2/htdocs/

EXPOSE 80
```

### Build & Run
```bash
docker build -t hello-apache .
docker run -d --name hello-apache-container -p 8081:80 hello-apache
```
Port `8081` on the host was mapped to port `80` inside the container. Accessed at: `http://localhost:8081`

### Output
![Apache Hello World output](<images/Screenshot 2026-08-31 190102.png>)

### Images

![Apache Hello World output](<images/Screenshot 2026-08-31 190102.png>)

The Apache web server successfully served the Hello World webpage.

---

## Docker Concepts Practiced

### Dockerfile Instructions

| Instruction | Purpose |
|---|---|
| `FROM` | Specifies the base image |
| `WORKDIR` | Sets the working directory inside the container |
| `COPY` | Copies files into the image |
| `RUN` | Executes commands during image creation |
| `EXPOSE` | Documents the port used by the application |
| `CMD` | Specifies the default command when the container starts |

### `docker build`
```bash
docker build -t <image-name> .
```
Creates a Docker image from a Dockerfile.

### `docker run`
```bash
docker run -d --name <container-name> -p <host-port>:<container-port> <image-name>
```
Creates and starts a container from an image.

### Port Mapping

Port mapping connects a host port to a container port. For example, the Python app mapped host port `5001` to container port `5000`, so the app listening on `5000` inside the container was reachable via `5001` on the host.

---

## Verification

List images:
```bash
docker images
```
List running containers:
```bash
docker ps
```

All four applications were successfully built and run using Docker.

---

## Directory Structure

```
docker-images/
├── apache-app/
│   ├── Dockerfile
│   └── index.html
├── java-app/
│   ├── Dockerfile
│   └── Main.java
├── nodejs-app/
│   ├── Dockerfile
│   ├── package.json
│   └── server.js
├── python-app/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
├── images/
│   ├── Screenshot (82).png
│   ├── Screenshot (84).png
│   ├── Screenshot (85).png
│   └── Screenshot 2026-08-31 190102.png
└── README.md
```

---

## Result

Four applications were successfully containerized using Docker — Node.js, Python, Java, and Apache — each built into an image, run as a container, and verified through a browser.

---

