# Dockerfiles & Images — Homework (Multi-Stage Build)

**Name:** Aditya Vikram Singh
**Roll No.:** 24bcs10429

---

## Task 1 — Run a Multi-Stage Dockerfile

### What the Dockerfile Does

- **Stage 1 (`build`)** — uses `node:18-alpine`, installs npm dependencies.
- **Stage 2 (`runtime`)** — a fresh `node:18-alpine` image that only copies over `node_modules`, `server.js`, and `package.json` from the build stage, keeping the final image small and free of build-only tooling.

### 1. Build the Image

From inside the project folder:
```bash
docker build -t multistage-app .
```

### 2. Run the Container
```bash
docker run -d --name multistage-container -p 8080:3000 multistage-app
```
This maps host port **8080** to the container's internal port **3000** (the port `server.js` listens on).

### 3. Access the Application

```
http://localhost:8080
```
Expected output:
```
Hello World from Docker multi-stage build
```

**Screenshot — Application Output**

![App running](<task1-multistage-build/Screenshot 2026-08-31 202559.png>)

### 4. Verify the Running Container
```bash
docker ps
```
The row for `multistage-container` shows `PORTS` as `0.0.0.0:8080->3000/tcp` — confirming the app is running on port 8080.

**Screenshot — `docker ps` Output**

![docker ps output](<task1-multistage-build/Screenshot 2026-08-31 202648.png>)

### Cleanup (optional)
```bash
docker stop multistage-container
docker rm multistage-container
```

---

## Task 2 — Documentation

**Name:** Aditya Vikram Singh
**Roll No.:** 24bcs10429

### Application Output

The application was built using a multi-stage Dockerfile and, once run, returns the expected message when accessed in the browser at `http://localhost:8080`.

![App running](<task1-multistage-build/Screenshot 2026-08-31 202559.png>)

*Expected output: `Hello World from Docker multi-stage build`*

### Running Container (`docker ps`)

The container is confirmed running and mapped to port 8080 via `docker ps`.

![docker ps output](<task1-multistage-build/Screenshot 2026-08-31 202648.png>)

*Port mapping confirmed: `0.0.0.0:8080->3000/tcp`*

### Notes

- Base image (build stage): `node:18-alpine`
- Base image (runtime stage): `node:18-alpine`
- Host port: `8080` → Container port: `3000`
- Image name: `multistage-app`
- Container name: `multistage-container`

---

## Task 3 — Deploying 3 Different Application Types with Docker

Three small, self-contained apps, each with its own Dockerfile:

| App | Folder | Port |
|---|---|---|
| Node.js | `nodejs-app/` | 3000 |
| Python (Flask) | `python-app/` | 5000 |
| Java | `java-app/` | 8000 |

### Node.js App
```bash
cd nodejs-app
docker build -t nodejs-app .
docker run -d --name nodejs-container -p 3000:3000 nodejs-app
curl http://localhost:3000
```
Expected: `Hello from the Node.js Docker app!`

![Node.js container output](<task3-multi-app-deployment/Screenshot 2026-08-31 203209.png>)

### Python App
```bash
cd python-app
docker build -t python-app .
docker run -d --name python-container -p 5000:5000 python-app
curl http://localhost:5000
```
Expected: `Hello from the Python Docker app!`

![Python container output](<task3-multi-app-deployment/Screenshot 2026-08-31 203705-1.png>)

### Java App
```bash
cd java-app
docker build -t java-app .
docker run -d --name java-container -p 8000:8000 java-app
curl http://localhost:8000
```
Expected: `Hello from the Java Docker app!`

![Java container output](<task3-multi-app-deployment/Screenshot 2026-08-31 203808.png>)

### Verify All Three Are Running Together
```bash
docker ps
```
All three containers — `nodejs-container`, `python-container`, and `java-container` — were `Up` simultaneously, each on its own port.

![All three containers running](<task3-multi-app-deployment/Screenshot 2026-08-31 203705.png>)

| Application | Image / Base | Host Port | Verified With |
|---|---|---|---|
| Node.js | `node:18-alpine` | 3000 | `curl http://localhost:3000` |
| Python | `python:3.12-slim` | 5000 | `curl http://localhost:5000` |
| Java | `eclipse-temurin:17-jre-alpine` | 8000 | `curl http://localhost:8000` |

### Cleanup (optional)
```bash
docker stop nodejs-container python-container java-container
docker rm nodejs-container python-container java-container
```

---

