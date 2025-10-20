# 🐳 Docker Registry Secret

A walkthrough demonstrating how to **deploy an application from a private Docker registry** by configuring a **Docker Registry Secret** in Kubernetes.

---

## 📘 Step 1 – Understanding Docker Registry Secrets

**Kubernetes uses a special type of Secret for authenticating to private registries.**  
This secret stores your Docker credentials securely, allowing Kubernetes to pull images from private repositories.

<br><br>

<p align="center">
  <img width="640" height="341" alt="docker-registry-secret-type" src="https://github.com/user-attachments/assets/f5e8a549-c419-42e0-a37c-54fa026e33fd" />
</p>

<br><br>

---

## 🚫 Step 2 – The Problem: Private Registry Without Credentials

**If you deploy a Pod or Deployment using an image from a private registry without providing credentials, it will fail to start.**

<br><br>

<p align="center">
  <img width="480" height="569" alt="deployment-failure" src="https://github.com/user-attachments/assets/0045c4d4-d1fc-4114-a30f-c69e4dd48aa4" />
</p>

<br><br>

---

## 🔑 Step 3 – Creating the Docker Registry Secret

**We create a secret of type `kubernetes.io/dockerconfigjson` that stores the registry credentials.**  
The credentials are encoded in Base64 and saved inside the Secret manifest.

<br><br>

<p align="center">
  <img width="1072" height="54" alt="create-secret" src="https://github.com/user-attachments/assets/48ee1a50-f9a4-4cc9-808c-f0dcd2f025ef" />
</p>

<br><br>

---

## ⚙️ Step 4 – Using the Secret in the Deployment

**Next, we update the Deployment specification to reference the secret via `imagePullSecrets`.**  
This allows the kubelet to authenticate and pull the image successfully.

<br><br>

<p align="center">
  <img width="365" height="183" alt="deployment-configuration" src="https://github.com/user-attachments/assets/903f7d21-6971-4555-a830-72310aa9ab7d" />
</p>

<br><br>

---

## ✅ Step 5 – Verifying Successful Deployment

**After applying the updated Deployment, the Pods should now pull images successfully and enter the `Running` state.**

<br><br>

<p align="center">
  <img width="411" height="83" alt="pods-running" src="https://github.com/user-attachments/assets/863bb46c-2fbb-425c-8994-455bc6394b4a" />
</p>

<br><br>

---

## 🧠 Key Takeaways

- Private registries require authentication for image pulls.  
- Use the secret type `kuberne
