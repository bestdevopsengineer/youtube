
apiVersion: v1
  kind: Pod
  metadata:
    name: nginx-pod
    labels:
      app: App1
      Function: Front-end
  
  spec:
    containers:
      - name: nginx-container
        image: nginx
        ports: 
          - containerPort: 8080
