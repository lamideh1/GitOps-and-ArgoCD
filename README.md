Sure, Olamide! Below is a clear, step-by-step **guide** to complete your **Mini Project on GitOps using ArgoCD in AWS (EKS)** — from scratch to submission.

---

## ✅ **PROJECT: Introduction to GitOps and ArgoCD in AWS**

---

### 🧰 **PREREQUISITES**

Make sure you have the following:

* ✅ AWS account with admin permissions
* ✅ `kubectl`, `eksctl`, `awscli` installed
* ✅ Git and GitHub account
* ✅ A working internet connection
* ✅ Docker (optional, for image building)

---

## 🔧 STEP-BY-STEP PROCEDURE

---

### **STEP 1: Create a Kubernetes Cluster (EKS)**

#### 📍 Where to Go:

* AWS Console: [https://console.aws.amazon.com/eks](https://console.aws.amazon.com/eks)
* OR use CLI:

#### 🔧 What to Do:

```bash
eksctl create cluster --name argo-cluster --region us-east-1 --nodes 2
```

> This creates a managed Kubernetes cluster with 2 worker nodes in `us-east-1`.

Wait 10–15 minutes for completion.

---

### **STEP 2: Install ArgoCD on the EKS Cluster**

#### 📍 Where to Go:

* Local terminal (run the commands below)

#### 🔧 What to Do:

```bash
# Create ArgoCD namespace
kubectl create namespace argocd

# Install ArgoCD core components
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

---

### **STEP 3: Access ArgoCD UI**

#### 📍 Where to Go:

* Local browser (for UI)
* Terminal (for port-forwarding)

#### 🔧 What to Do:

```bash
# Forward ArgoCD UI port
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Visit:

```
http://localhost:8080
```

#### 🔑 Get Login Credentials:

```bash
kubectl get secret argocd-initial-admin-secret -n argocd \
-o jsonpath="{.data.password}" | base64 -d
```

* **Username**: `admin`
* **Password**: (paste decoded password above)

---

### **STEP 4: Deploy a Sample Application via ArgoCD**

#### 📍 Where to Go:

* GitHub: Fork or clone this repo:
  [https://github.com/argoproj/argocd-example-app](https://github.com/argoproj/argocd-example-app)
* ArgoCD UI (Applications → NEW APP)

#### 🔧 What to Do:

1. On ArgoCD UI, click **NEW APP**:

   * App Name: `guestbook`
   * Project: `default`
   * Sync Policy: `Automated`
   * Repo URL: `https://github.com/argoproj/argocd-example-app`
   * Path: `.`
   * Revision: `HEAD`
   * Cluster: `https://kubernetes.default.svc`
   * Namespace: `default`
2. Click **Create**

🎯 It should deploy and sync automatically.

---

### **STEP 5: Monitor Deployment**

#### 📍 Where to Go:

* ArgoCD UI → Applications → `guestbook`

#### 🔧 What to Do:

* Observe sync status
* Click “App Details” to view resources
* Click “Sync” or “Refresh” as needed
* Modify repo and observe automatic sync

---

### **STEP 6: Add a Change and Push to Git**

#### 📍 Where to Go:

* GitHub (edit file)
* ArgoCD (see sync)

#### 🔧 What to Do:

* Change a value in the YAML file, e.g., change `replicas: 1` to `replicas: 2`
* Commit and push
* ArgoCD will automatically detect and sync it

---

### **STEP 7: Document Everything in a README.md**

#### 📍 Where to Go:

* Your project GitHub repo

#### 🔧 What to Include:

* Project Overview
* GitOps principles summary
* EKS cluster setup steps
* ArgoCD installation and access instructions
* App deployment steps
* Sync & rollback demonstration
* Challenges and resolutions

---

### **STEP 8: Submit Your Work**

#### 📍 Where to Go:

* Your course portal (submit repo URL)
* Include README.md and screenshots in the repo

#### 🔧 What to Provide:

* GitHub repository link
* Brief report (in README or separate doc) with:

  * Strategy
  * What you learned
  * Challenges faced
  * Screenshots

---

## 🗂️ Recommended Folder Structure:

```
argocd-gitops-mini-project/
├── guestbook-app.yaml
├── screenshots/
│   ├── eks-cluster.png
│   ├── argocd-ui.png
│   ├── deployed-app.png
├── README.md
```

---

## 🚀 Need Help?

If you want me to:

* Write your `README.md`
* Provide a sample GitHub repo
* Help create screenshots placeholders

Let me know, and I’ll generate them for you.

Would you like me to generate a sample `README.md` now?
