## **Dockerfile – all important instructions in order**
#### 1. FROM: Defines the base image (starting point) 
Why: Every image needs a foundation (like OS or runtime) 
* `FROM ubuntu:20.04` → Base image
---
####  2. LABEL: Adds metadata to image / Adds info about image (owner, version)
Why: Helps in documentation and management 
* `LABEL maintainer="priyanka@example.com"` → Metadata
---
####  3. ENV: Sets environment variables 
Why: Used for configuration inside container (like config values)
* `ENV APP_ENV=production` → Set environment variable
---
#### 4. ARG:  Build-time variable. 
Why: Used during image build only (not runtime) /  Pass values during image build (`docker build --build-arg`)
* `ARG VERSION=1.0` → Build-time variable
---
#### 5. WORKDIR: Sets working directory inside container 
Why: Avoid writing full paths again and again

What actually happens when you use WORKDIR?
WORKDIR = "cd + mkdir (if needed)" automatically. Inside container image WORKDIR /app
* `WORKDIR /app` → Set working directory. What it does: Sets /app as the current working directory inside the container  All next commands (RUN, CMD, COPY) will run inside /app
* If /app does NOT exist → Docker will automatically create it. If /app already exists → Docker will just use it. So you don’t need to create it manually.
* 


What happens and how its work:
```
Start container from Ubuntu image 
WORKDIR /app #Docker checks: does /app exist?  No → creates /app 
COPY . . # copies into /app
RUN touch file.txt #File created inside /app or runs inside /app
Final path: /app/file.txt
```

Multiple WORKDIR example: Docker builds nested directories automatically
```
WORKDIR /app
WORKDIR logs
WORKDIR today
Result: /app → created, /app/logs → created, /app/logs/today → created 
```
Important Behavior:  Relative vs Absolute path
```
WORKDIR /app
WORKDIR test
Result: /app/test
```
- How to access WORKDIR: Inside container: docker exec -it container_name bash --->  cd /app
-	WORKDIR sets working directory inside container 
-	Automatically creates directory if not exists 
-	Supports relative paths 
-	Affects RUN, CMD, COPY, ENTRYPOINT 
- Cleaner than using cd in RUN 
---
####  6. COPY: Copies files from local to container 
Why: Used to move / add application code into image 
* `COPY . /app` → Copy files from local to container
* First, we clone the GitHub repository to local or CI server. Then we navigate to the project directory and build the Docker image using docker build. Docker requires local build context to copy files into the image.
* Clone repo → go inside folder → build image
* If you are working manually (your laptop): Yes, you must clone the repo
* If you are using CI/CD (Jenkins, GitHub Actions):  You don’t clone manually. But system automatically clones
* Yes, we usually clone the repository before building the Docker image because Docker requires a local build context. In CI/CD pipelines, the cloning is handled automatically by tools like Jenkins.
* Flow: Developer pushes code → GitHub Jenkins triggers pipeline
* Jenkins does:
```
git clone repo
cd project
docker build -t myapp .
docker push myapp
``` 
---
####  7. ADD: Similar to COPY but supports URL & auto-extract 
Why: Useful for downloading or extracting files / Advanced copy (but mostly avoid, use COPY)
* `ADD app.tar.gz /app` → Copy + auto-extract / URL support
---
####  8. RUN: Executes commands during image build 
Why: Used to install packages/ software or setup environment and dependencies. To prepare the image
* `RUN apt update && apt install -y python3` → Execute command at build time
---
####  9. EXPOSE: Defines port used by container 
Why: Inform which port app runs on (not actually publish) /Helps in communication (documentation purpose) 
* `EXPOSE 8080` → Declare port
---
####  10. VOLUME: Creates mount point for persistent data 
Why: Persist data outside container/ Data is not lost when container is removed 
* `VOLUME /data` → Create mount point
---
#### 11. USER: Specifies user to run container 
Why: Improves security (avoid root user) 
* `USER appuser` → Run container as specific user
---
#### 12. CMD: Default command to run when container starts 
Why: Tells container what to execute at runtime / Runs when container starts (can override)
* `CMD ["python3", "app.py"]` → Runs python app.py and Starts your application/ Default command
Always run: Main application, Server process (Starts Nginx web server), Long-running process
``` docker run myapp ```
Docker does: Creates container --> Starts container and Executes CMD instruction
---
#### 13. ENTRYPOINT: Sets main command (like fixed executable) 
Why: Ensures container always runs specific command / Makes container behave like executable
* `ENTRYPOINT ["python3"]` → Fixed main command
---
#### 14. HEALTHCHECK: Why: Check container health status
* `HEALTHCHECK CMD curl --fail http://localhost:8080 || exit 1`
---
#### 15. ONBUILD: Executes instruction when image is used as base 
Why: Used for reusable base images
* `ONBUILD COPY . /app` → Trigger when used as base image
---

## Full Example Dockerfile (Real Scenario)

```dockerfile
FROM python:3.9
LABEL maintainer="priyanka@example.com"
ENV APP_ENV=production
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]
```

---

### Simple Order to Remember
FROM → LABEL → ARG → ENV → WORKDIR → COPY/ADD → RUN → EXPOSE → VOLUME → USER → CMD/ENTRYPOINT
---
### Important Tips
* Use `COPY` instead of `ADD` (best practice)
* Combine `RUN` commands to reduce layers
* Use `CMD` for default, `ENTRYPOINT` for fixed command
* Keep image size small (use slim/alpine images)

---


