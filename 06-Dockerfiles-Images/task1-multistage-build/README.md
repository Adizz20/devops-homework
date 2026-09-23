# Task 1 — Multi-stage Dockerfile

This folder is a ready-to-use multi-stage Docker app. If your assignment
requires cloning a specific instructor-provided repo instead, replace these
files with that repo's contents and skip to "Build the image" below — the
commands are the same.

## What the Dockerfile does

- **Stage 1 (`build`)**: uses `node:18-alpine`, installs npm dependencies.
- **Stage 2 (`runtime`)**: a fresh `node:18-alpine` image that only copies
  over `node_modules`, `server.js`, and `package.json` from the build stage.
  This keeps the final image small and free of build-only tooling.

## 1. (If cloning an external repo) Clone it

```bash
git clone <repository-url>
cd <repository-folder>
```

## 2. Build the image

From inside `task1-multistage-build/`:

```bash
docker build -t multistage-app .
```


## 3. Run the container

```bash
docker run -d --name multistage-container -p 8080:3000 multistage-app
```

This maps host port **8080** to the container's internal port 3000 (the port
`server.js` listens on).

## 4. Access the application

Open a browser (or use curl) at:

```
http://localhost:8080
```

You should see:

```
Hello World from Docker multi-stage build
```

![alt text](<Screenshot 2026-08-31 202559.png>)

## 5. Verify the running container

```bash
docker ps
```

Confirm the row for `multistage-container` shows `PORTS` as
`0.0.0.0:8080->3000/tcp` — this is your evidence the app is running on
port 8080.

![alt text](<Screenshot 2026-08-31 202648.png>)

## Cleanup (optional, after you're done)

```bash
docker stop multistage-container
docker rm multistage-container
```

## Aditya Vikram Singh
24bcs10429