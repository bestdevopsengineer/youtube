apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    - dev

specs:
  containers:
    - name: nginx-container
      image: nginx
