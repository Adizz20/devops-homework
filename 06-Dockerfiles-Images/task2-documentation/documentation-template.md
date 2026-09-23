# Docker Multi-Stage Build — Submission

**Name:** Aditya Vikram Singh
**Enrollment number:** 24bcs10429

---

## Task 1 — Multi-stage Dockerfile

### Application output

The application was built using a multi-stage Dockerfile and, once run,
returns the expected message when accessed in the browser at
`http://localhost:8080`.

![App running](./screenshots/Screenshot%202026-08-31%20202559.png)

*Expected output: `Hello World from Docker multi-stage build`*

### Running container (docker ps)

The container is confirmed running and mapped to port 8080 via `docker ps`.

![docker ps output](./screenshots/image-1.png)

*Port mapping confirmed: `0.0.0.0:8080->3000/tcp`*

---

## Notes

- Base image (build stage): `node:18-alpine`
- Base image (runtime stage): `node:18-alpine`
- Host port: `8080` → Container port: `3000`
- Image name: `multistage-app`
- Container name: `multistage-container`

---

## Task 3 — Multiple application types deployed with Docker

| Application | Image / base | Host port | Verified with |
|---|---|---|---|
| Node.js     | `node:18-alpine`   | 3000 | `curl http://localhost:3000` |
| Python      | `python:3.12-slim` | 5000 | `curl http://localhost:5000` |
| Java        | `eclipse-temurin:17-jre-alpine` | 8000 | `curl http://localhost:8000` |

![All containers running](./screenshots/image.png)

*All three containers running simultaneously, each on its own port.*
