# 📦 Packaging a Simple Website with Nginx and Docker

## 📝 Description
This guide walks you through the steps to package and deploy a simple static website using **Nginx** and **Docker**.

---

## 1. Create the project directory and required files

First, create a directory to store your website and the necessary files.  
In this example, we only need one HTML file.

```bash
mkdir my-web && cd my-web   # Create the "my-web" directory and move into it
touch index.html            # Create the HTML file
touch Dockerfile            # Create the Docker configuration file
```
---

## 2. Create a simple HTML webpage

This is your website. When accessed, the browser will display the content of this file.

The file must be placed in a directory that Nginx can read.

Open index.html and add the following content:
```
<h1>Hello I'm from lab Mrs. Ha!</h1>
<p>This website is running in Docker Container with Nginx!</p>
```

---

## 3. Write the Dockerfile to build a Docker Image
A Dockerfile is a recipe used to build a Docker Image.

We will use Nginx as the web server.

The index.html file needs to be copied into Nginx’s default web directory so it can be served.

Open Dockerfile and add the following content:
```dockerfile
# Use the latest Nginx image as the base image
FROM nginx:latest  

# Copy index.html into Nginx default web directory
COPY index.html /usr/share/nginx/html/index.html  

# Expose port 80 (default HTTP port)
EXPOSE 80  

# Run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
```

### 🔍 Explanation

1️⃣ `FROM nginx:latest` → Pulls the latest Nginx image from Docker Hub.
2️⃣ `COPY index.html /usr/share/nginx/html/index.html` → Copies the website file into Nginx’s default serving directory.
3️⃣ `EXPOSE 80` → Exposes port 80 for HTTP traffic.
4️⃣ `CMD ["nginx", "-g", "daemon off;"]` → Runs Nginx in foreground mode so the container keeps running. 

---

## 4. Build the Docker Image
Now we build a Docker Image from the Dockerfile.

Docker will:
- Pull the Nginx image
- Copy index.html
- Create a runnable image

Run the following command:
```bash
docker build -t my-nginx .
```

🔍 **Command explanation:**
- `docker build` → Builds a Docker image
- `-t my-nginx` → Names the image **my-nginx**.
- `.` → Uses the Dockerfile in the current directory

⏳ **If successful, the build process will finish without errors: `FINISHED`!**

---

## 5. Run a Container from the Image

Now we run a container from the image we just built.

The container will use Nginx to serve the website.

We map port 8080 on the host machine to port 80 inside the container.

Run the following command:
```bash
docker run -d -p 8080:80 my-nginx
```

Command explanation

1️⃣ docker run → Starts a new container

2️⃣ -d → Runs the container in detached (background) mode

3️⃣ -p 8080:80 → Port mapping:

Host port 8080 → Container port 80

4️⃣ my-nginx → The Docker image name

✅ After running this command, the container is running and the website is live.

## 6. Access the website

Open your browser and go to:
```
http://localhost:8080  
```
🎉 You should see your webpage served by Nginx running inside a Docker container.

