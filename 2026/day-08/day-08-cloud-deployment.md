# Day 08 – Cloud Server Setup: Nginx & Web Deployment

## Objective

Today I practiced deploying and checking a web server on an AWS EC2 cloud server.

I worked with:

- AWS EC2
- Ubuntu Linux
- Nginx
- SSH
- HTTP port 80
- Nginx logs
- Docker
- Basic troubleshooting commands

---

## Cloud Server

My server is running Ubuntu Linux on AWS EC2.

I connected to the server using SSH and checked the server hostname.

### Check Hostname

```bash
hostname
```

Output:

```text
ip-172-31-33-72
```

---

## Nginx Installation and Status

I checked whether Nginx was running.

```bash
systemctl status nginx
```

### Result

Nginx was active and running successfully.

The service showed:

```text
Active: active (running)
```

I also checked the webpage locally:

```bash
curl localhost
```

The command returned the HTML/CSS content of my webpage.

---

## Check Port 80

I checked whether Nginx was listening on HTTP port 80.

```bash
ss -tulpn | grep :80
```

Port 80 was listening, which means the Nginx web server was accepting HTTP connections.

---

## Test Web Access

I configured the AWS Security Group to allow HTTP traffic on port 80.

I then opened the EC2 public IP address in my browser:

```text
http://<PUBLIC-IP>
```

The webpage loaded successfully.

I captured a screenshot of the webpage as:

```text
nginx-webpage.png
```

---

## Nginx Logs

I checked the Nginx access logs:

```bash
sudo tail -n 50 /var/log/nginx/access.log
```

The access log showed HTTP requests received by Nginx.

I also checked the Nginx error log:

```bash
sudo tail -n 50 /var/log/nginx/error.log
```

The error log can be used to investigate Nginx problems.

### Observed Traffic

The access logs showed automated Internet scanning requests.

Some requests attempted to access common sensitive files and paths such as:

```text
/laravel/.env
/backend/.env
/admin/.env
/config/.env
/wp-config.php.bak
/docker-compose.yml
/.github/workflows/build.yml
/appsettings.json
/config/production.json
/phpinfo.php
/info.php
```

These requests returned `404` responses, meaning the requested resources were not found.

The logs also showed successful requests to `/` returning `200`, confirming that the webpage was being served successfully.

---

## Save Nginx Logs

I saved the latest 50 access log entries into a separate file.

```bash
sudo tail -n 50 /var/log/nginx/access.log > nginx-logs.txt
```

I verified the contents:

```bash
cat nginx-logs.txt
```

I also checked the file size:

```bash
ls -lh nginx-logs.txt
```

The file was successfully created and contained the latest Nginx access log entries.

---

# Docker Installation and Verification

## Initial Docker Check

As part of the exercise, I checked whether Docker was already installed on the server.

```bash
docker --version
```

Docker was not installed initially.

The server returned:

```text
Command 'docker' not found
```

This confirmed that Docker needed to be installed.

---

## Update Ubuntu Packages

I updated the Ubuntu package lists:

```bash
sudo apt update
```

The package lists were updated successfully.

---

## Install Docker

I installed Docker using the Ubuntu package:

```bash
sudo apt install docker.io -y
```

Docker and its required dependencies were installed successfully.

---

## Start Docker

After installation, I started the Docker service:

```bash
sudo systemctl start docker
```

---

## Enable Docker

I enabled Docker so that it starts automatically when the server boots:

```bash
sudo systemctl enable docker
```

---

## Check Docker Version

I verified the Docker installation:

```bash
docker --version
```

Output:

```text
Docker version 29.1.3, build 29.1.3-0ubuntu4.1
```

This confirmed that Docker was successfully installed.

---

## Check Docker Service

I checked the Docker service status:

```bash
sudo systemctl status docker
```

The service showed:

```text
Active: active (running)
```

This confirmed that the Docker daemon was running successfully.

---

## Test Docker Installation

I tested Docker using the `hello-world` image:

```bash
sudo docker run hello-world
```

Docker successfully pulled and ran the `hello-world` image.

The output included:

```text
Hello from Docker!
```

This confirmed that:

1. The Docker client could communicate with the Docker daemon.
2. Docker could pull an image from Docker Hub.
3. Docker could create a container.
4. Docker could run the container successfully.

Therefore, the Docker installation was working correctly.

---

## Docker Commands Used

The main Docker commands I used were:

```bash
docker --version
```

```bash
sudo apt update
```

```bash
sudo apt install docker.io -y
```

```bash
sudo systemctl start docker
```

```bash
sudo systemctl enable docker
```

```bash
sudo systemctl status docker
```

```bash
sudo docker run hello-world
```

---

## Commands Used

### Server and Nginx

```bash
hostname
```

```bash
systemctl status nginx
```

```bash
curl localhost
```

```bash
ss -tulpn | grep :80
```

```bash
sudo tail -n 50 /var/log/nginx/access.log
```

```bash
sudo tail -n 50 /var/log/nginx/error.log
```

```bash
sudo tail -n 50 /var/log/nginx/access.log > nginx-logs.txt
```

```bash
cat nginx-logs.txt
```

```bash
ls -lh nginx-logs.txt
```

### Docker

```bash
docker --version
```

```bash
sudo apt update
```

```bash
sudo apt install docker.io -y
```

```bash
sudo systemctl start docker
```

```bash
sudo systemctl enable docker
```

```bash
sudo systemctl status docker
```

```bash
sudo docker run hello-world
```

---

## Challenges Faced

One thing I learned was that the server has a private IP address and a public IP address.

The private IP is used inside the AWS network, while the public IP is used to access the web server from the Internet.

I also learned that the AWS Security Group needs to allow HTTP traffic on port 80 for the webpage to be accessible.

Another challenge was that Docker was not installed initially.

When I ran:

```bash
docker --version
```

the server returned:

```text
Command 'docker' not found
```

I then installed Docker using:

```bash
sudo apt install docker.io -y
```

After installation, I started and enabled the Docker service and verified it using:

```bash
sudo docker run hello-world
```

The `hello-world` container ran successfully, confirming that Docker was working.

---

## What I Learned

- I learned how to connect to an AWS EC2 server using SSH.
- I learned how to check whether Nginx is running using `systemctl`.
- I learned how to test a web server using `curl`.
- I learned that HTTP normally uses port 80.
- I learned how AWS Security Groups control inbound traffic.
- I learned how to check Nginx access and error logs.
- I learned how to save command output into a text file using `>`.
- I learned that public web servers can receive automated scanning requests from the Internet.
- I learned how to install Docker on Ubuntu using `apt`.
- I learned how to start and enable the Docker service.
- I learned how to check the Docker version.
- I learned how to verify Docker using the `hello-world` container.
- I learned the basic relationship between Docker, images, containers, and the Docker daemon.

---

## DevOps Takeaway

A web server deployment is not only about installing Nginx.

I need to check:

1. Is the service running?
2. Is the correct port listening?
3. Is the cloud firewall/security group allowing traffic?
4. Can I access the webpage?
5. What do the logs show?
6. Are the required tools and services installed and working?

This gives me a basic troubleshooting flow for a real cloud server.

Docker also demonstrated an important part of DevOps: installing a container runtime, managing its service, and verifying that containers can be created and executed successfully.

---

## Evidence

The following files/screenshots were collected for this exercise:

- `ssh-connection.png`
- `nginx-webpage.png`
- `nginx-logs.png`
- `nginx-logs.txt`

Docker was also verified directly on the EC2 server using:

```bash
sudo docker run hello-world
```

The terminal output showed:

```text
Hello from Docker!
```

This served as proof that Docker was installed and working.

---

## Day 08 Summary

Today I practiced working with an AWS EC2 cloud server, checking Nginx, testing HTTP access, collecting Nginx logs, and installing and verifying Docker.

I learned how to check services, verify listening ports, troubleshoot web access, inspect server logs, and save command output to files.

The Nginx logs also showed automated Internet scanning activity, which helped me understand why monitoring logs and properly securing publicly accessible cloud servers is important.

Docker was not installed initially, so I installed it using Ubuntu's `docker.io` package. I started and enabled the Docker service, checked the installed version, verified that the service was running, and successfully ran the `hello-world` container.

This helped me understand the basic workflow of deploying and troubleshooting web services and container tools in a cloud environment.
