# 🎮 2048 Game — Containerized & Deployed on AWS

> A classic 2048 puzzle game fully containerized with Docker and deployed to the cloud using AWS services. Built to practice real-world DevOps deployment workflows.

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![AWS EC2](https://img.shields.io/badge/AWS_EC2-FF9900?style=flat-square&logo=amazonec2&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Docker Hub](https://img.shields.io/badge/Docker_Hub-2496ED?style=flat-square&logo=docker&logoColor=white)

---

## 🧩 The Problem

Deploying a web app manually is fragile — it works on your machine but breaks in production. This project tackles that by containerizing the app with Docker, so it runs identically everywhere, then pushing it to the cloud for public access.

---

## 🏗️ Architecture

```
User Browser
     │
     ▼
AWS EC2 Instance (Ubuntu)
     │
     ▼
Docker Container
     │
     ▼
Nginx (serves the 2048 game on port 80)
```

**Flow:**
1. Game code is packaged into a Docker image
2. Image is pushed to Docker Hub
3. EC2 instance pulls the image and runs the container
4. Nginx inside the container serves the game publicly on port 80
5. AWS Security Group opens port 80 for inbound HTTP traffic

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Docker | Containerize the game |
| Docker Hub | Store & distribute the image |
| AWS EC2 (Ubuntu 22.04) | Cloud server to run the container |
| Nginx | Web server inside the container |
| AWS Security Groups | Control inbound network access |

---

## 🚀 How to Deploy It Yourself

### Prerequisites
- AWS account (Free Tier works)
- Docker installed locally
- Docker Hub account

### Step 1 — Build the Docker Image
```bash
git clone https://github.com/sneha020902/AWS-2048-game.git
cd AWS-2048-game
docker build -t 2048-game .
```

### Step 2 — Push to Docker Hub
```bash
docker tag 2048-game your-dockerhub-username/2048-game
docker push your-dockerhub-username/2048-game
```

### Step 3 — Launch an EC2 Instance
- Go to AWS Console → EC2 → Launch Instance
- Choose **Ubuntu 22.04 LTS** (Free Tier eligible)
- In Security Group, allow **port 80 (HTTP)** and **port 22 (SSH)**

### Step 4 — SSH into EC2 and Run the Container
```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip

# Install Docker on EC2
sudo apt update && sudo apt install -y docker.io
sudo systemctl start docker

# Pull and run the container
sudo docker pull your-dockerhub-username/2048-game
sudo docker run -d -p 80:80 your-dockerhub-username/2048-game
```

### Step 5 — Access the Game
Open your browser and navigate to:
```
http://your-ec2-public-ip
```

---

## 💡 What I Learned

- How to write a **Dockerfile** and build a container image from scratch
- How to push images to **Docker Hub** and pull them on a remote server
- How to launch and configure an **AWS EC2** instance from scratch
- How **AWS Security Groups** control network traffic
- How **Nginx** serves static web content inside a container
- The full **build → push → pull → run** Docker deployment cycle

---

## 🔮 Future Improvements

- [ ] Add HTTPS using Let's Encrypt + Certbot
- [ ] Deploy on **AWS ECS** (Elastic Container Service) for scalability
- [ ] Set up a **custom domain** with AWS Route 53
- [ ] Add a **CI/CD pipeline** with GitHub Actions to auto-deploy on push

---

## 👩‍💻 Author

**Sneha Agrawal** — Aspiring Cloud & DevOps Engineer  
🔗 [LinkedIn](https://www.linkedin.com/in/-snehaagrawal/) · [GitHub](https://github.com/sneha020902) · [Portfolio](https://sneha020902.github.io)
