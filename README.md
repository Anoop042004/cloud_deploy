# Blogify - Node.js Blogging Platform

Blogify is a simple and scalable blogging application built with Node.js and connected to MongoDB Atlas for database storage. It provides a clean RESTful API backend to create, read, update, and delete blog posts.

This project has been deployed on multiple platforms including:  
- **Google Cloud VM (IaaS)** — manual deployment on a virtual machine  
- **Render.com (PaaS)** — platform-as-a-service for easy hosting without infrastructure management  

## Deploying Blogify  on Google Cloud VM(IaaS)

## Steps to Deploy

### 1. Create a VM on GCP  
- Go to **Compute Engine > VM Instances > Create Instance**  
- Configure the VM with:  
  - Machine type: **e2-medium** (2 vCPUs, 4GB RAM)  
  - Operating System: **Ubuntu 22.04 LTS**  
  - Enable **Allow HTTP traffic** and **Allow HTTPS traffic**  

### 2. Connect to the VM  
- Use the **SSH** button in the GCP Console to open a terminal  

### 3. Install Node.js and npm  
```bash
sudo apt update
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install nodejs -y
node -v
npm -v
```

### 4. Clone your Blogify repository and navigate inside  
```bash
git clone https://github.com/Anoop042004/cloud_deploy.git
cd blogify
```

### 5. Install dependencies  
```bash
npm install
```

### 6. Start the Node.js application  
```bash
node app.js
```

### 7. Access your running app  
- Open your VM’s external IP address in a browser with the port your app uses (default 3000):  
```
http://EXTERNAL_IP:3000
```

---

## Firewall Configuration Note  

If you cannot access your app externally, you may need to open your app’s port in the Google Cloud firewall:  

1. Go to **VPC Network > Firewall** in the Google Cloud Console.  
2. Click **Create Firewall Rule**.  
3. Configure:  
   - **Name:** allow-nodejs-3000 (or any name you choose)  
   - **Targets:** All instances in the network (or specify your VM)  
   - **Source IP ranges:** 0.0.0.0/0 (allows all IPs; restrict as needed)  
   - **Protocols and ports:** Select **Specified protocols and ports** → check **tcp** → enter **3000**  
4. Click **Create**.  

After this, your app should be accessible via `http://EXTERNAL_IP:3000`.

---

## Notes  
- Replace `EXTERNAL_IP` with your actual VM’s external IP from the GCP console.  
- Ensure your MongoDB Atlas cluster allows connections from your VM’s IP or is open for your testing setup.  

---
## Deploying Blogify on Render (PaaS)

This guide covers how to deploy the Blogify Node.js backend application on Render, a platform-as-a-service (PaaS) provider that simplifies app hosting with minimal infrastructure management.

## Steps to Deploy on Render

### 1. Create a Render Account  
- Go to https://render.com and sign up or log in.

### 2. Create a New Web Service  
- Click **New** > **Web Service**.  
- Connect your GitHub repository containing Blogify.

### 3. Configure the Service  
- Select the repository and branch to deploy (e.g., `main`).  
- Set the **Environment** to **Node**.  
- Specify the **Build Command**:  
  ```bash
  npm install
  ```  
- Specify the **Start Command**:  
  ```bash
  node app.js
  ```  
- Choose the **Region** closest to your users.



### 4. Deploy the Service  
- Click **Create Web Service**.  
- Render will build and deploy your app automatically.

### 5. Access Your Application  
- Once deployed, Render provides a public URL (e.g., `https://your-app.onrender.com`).  
- Visit this URL to use your Blogify app.

---

## Notes  
- Render automatically handles server management, scaling, and HTTPS.  
- You can view logs and restart the service via the Render dashboard.  
- To update the app, push changes to the connected GitHub branch — Render redeploys automatically.

---
