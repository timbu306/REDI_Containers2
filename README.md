# 🚀 Explore Kubernetes Beyond Basics — Fun Self-Study Activity

Welcome to your last Cloud Infrastructure session! You've done great with Minikube. Now let's explore Kubernetes components a bit deeper to see how real cloud applications run and scale. This activity takes about **60-90 minutes** and builds your confidence with Kubernetes concepts by practical, hands-on steps.

---

## Step 1: Review Your Minikube Cluster Status (5 min)

Let's start your Kubernetes cluster and check that everything is ready.

**Run this to start Minikube:**

```bash
minikube start
```

**Check the status of your cluster:**

```bash
minikube status
```

### Why?
This starts your tiny Kubernetes cloud on your computer—it's your little mini data center. Verifying the status ensures your Kubernetes brain (control plane) and worker nodes (where containers run) are ready.

---

## Step 2: Deploy a Simple Application with Labels (15 min)

Deploy the nginx web server like before, but now add a label to the deployment.

```bash
kubectl create deployment webserver --image=nginx:latest --labels="app=webserver,env=dev"
```

**Check the pods and their labels:**

```bash
kubectl get pods --show-labels
```

### Why?
Labels are important to organize and manage your apps inside Kubernetes. They act like name tags telling Kubernetes which objects belong together, helping with updates, scaling, and monitoring.

---

## Step 3: Create a Service to Access Your App (10 min)

Expose your deployment so you can open the web server in your browser.

```bash
kubectl expose deployment webserver --type=NodePort --port=80
```

**Get the URL to open the web server:**

```bash
minikube service webserver --url
```

Open the URL in your browser.

### Why?
Services expose your app inside and outside Kubernetes. The NodePort service makes your app reachable from your computer's web browser. This mimics how web apps are accessible on the internet.

---

## Step 4: Scale Your Application (10 min)

Let's make your app handle more visitors by increasing the number of webserver pods.

```bash
kubectl scale deployment webserver --replicas=4
```

**Check that 4 pod copies are running:**

```bash
kubectl get pods
```

### Why?
Scaling means running multiple copies (pods) of your app for more reliability and capacity. Kubernetes automatically balances traffic between these copies, like many shop assistants helping customers.

---

## Step 5: Rolling Updates — Upgrade Your App Without Downtime (20 min)

Apply an update to your app by switching the nginx image version.

```bash
kubectl set image deployment/webserver nginx=nginx:1.23
```

**Watch the update rolling out gracefully:**

```bash
kubectl rollout status deployment/webserver
```

### Why?
Rolling updates let you upgrade apps without interruption. Kubernetes replaces old pods with new ones one by one, so the app stays available continuously.

---

## Step 6: Inspect Logs and Connect to Your App (15 min)

**Find your pod name:**

```bash
kubectl get pods -l app=webserver -o jsonpath="{.items[0].metadata.name}"
```

**Check logs of the pod:**

```bash
kubectl logs <pod-name>
```

**Connect inside the pod's container:**

```bash
kubectl exec -it <pod-name> -- /bin/sh
```

**Inside, list nginx web files:**

```bash
ls /usr/share/nginx/html
exit
```

### Why?
Logs help you understand what the app is doing and where errors might happen. Exec lets you jump inside a running app to troubleshoot or explore the file system — essential for real-world cloud operators.

---

## Step 7: Cleanup (5 min)

When done, delete your app and stop Kubernetes:

```bash
kubectl delete service webserver
kubectl delete deployment webserver
minikube stop
```

### Why?
Clean environments keep your computer tidy and ensure no leftover resources consume memory or CPU.

---

## Extra Challenge (Optional)

Try editing the nginx HTML page inside the pod by using `kubectl exec` to open a shell, then modify files with basic Linux commands (`echo`, `cat`). Or, try deploying a different app from Docker Hub!

---

## Summary of What You Built and Learned

| Component | What It Is | Why It Matters |
|-----------|------------|----------------|
| Minikube cluster | Tiny Kubernetes in your PC | Learn how a cloud platform works locally |
| Deployment + Labels | Running app copies with identity | Organize, scale, and update your apps |
| Service (NodePort) | Access point to your app | Connect apps to users inside/outside |
| Scaling | Multiple copies of your app | Improve availability and performance |
| Rolling updates | Safe app upgrades | Keep apps running while upgrading |
| Logs + Exec | Inspect app internals and troubleshoot | Understand and fix app behavior |

---

## Tips for Success

- Take your time and try commands twice if unsure.
- Use official links to learn more if curious (below).
- Save command outputs as notes for your records.

---

## Helpful Links (for later reading)

- [Kubernetes concepts](https://kubernetes.io/docs/concepts/)
- [kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [Minikube docs & drivers](https://minikube.sigs.k8s.io/docs/)

---

**You've done a great job learning cloud infrastructure basics and Kubernetes! Keep practicing and exploring. Your next step learning cloud native architecture starts here!** 🎓🚀
