
## Step 1: Inspect Dockerfile
Inspected the Dockerfile to understand the base image, application setup, exposed ports, and container startup command for the Node.js application.

---

## Step 2: Build Docker Image
Built the Docker image using the following command:
```bash
docker build -t nodejs-hello-world:1.0 .
```

Verified the image was created successfully using:
```bash
docker images
```
---
## Step 3: Run the Container

Ran the container in detached mode and mapped host port **80** to container port **3000**:

```bash
docker run -d -p 3000:3000 --name nodejs-hello nodejs-hello-world:1.0
```
---
## Step 4: Verify Application Accessibility
Verified the application was accessible by sending an HTTP request using curl:
```bash
curl http://localhost:3000
```
## ## Step 5: Verify Container Status
Checked the running container status to ensure the container was running correctly:
```bash
docker ps
```
## ## Step 6: Retrieve Application Logs
Retrieved and reviewed the application logs to confirm successful startup and no runtime errors:
```bash
docker logs nodejs-hello
```
## ## Step 7: Save Docker Image
Saved the Docker image to a tar archive for backup and portability:
```bash
docker save -o nodejs-hello-world-1.0.tar nodejs-hello-world:1.0
```
## ## Step 8: Cleanup
Stopped and removed the running container after verification:
```bash
docker stop nodejs-hello
docker rm nodejs-hello
```
