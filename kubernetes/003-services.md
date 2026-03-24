
apiVersion: v1
kind: Services
metadata:
  name: nginx-svc
  labels:
    app: nginx-svc-label

spec:
  containers:
    - name: nginx-container
      image: nginx


<img width="1020" height="347" alt="image" src="https://github.com/user-attachments/assets/242ff86d-c2a1-4faa-9ca9-89a0dc8a8866" />
