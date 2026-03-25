<img width="788" height="487" alt="image" src="https://github.com/user-attachments/assets/0abb8fda-3283-4be6-96d4-0f9bcfcf0844" />
<img width="1087" height="516" alt="image" src="https://github.com/user-attachments/assets/7e75d726-e4f1-4b84-8063-e33192d1a3c2" />
<img width="1082" height="422" alt="image" src="https://github.com/user-attachments/assets/fdf97ab9-8845-4016-9d13-8ab271373252" />

# horizontal pod autoscaler (HPA)
<img width="996" height="510" alt="image" src="https://github.com/user-attachments/assets/9e07ff75-f123-4647-a1ae-d42c2a230d62" />
<img width="856" height="456" alt="image" src="https://github.com/user-attachments/assets/6c6fb831-68c4-40b6-823c-760c1e26bb9d" />
<img width="1022" height="485" alt="image" src="https://github.com/user-attachments/assets/10142694-118a-4b54-8ebd-fe22fcbe7364" />
<img width="892" height="447" alt="image" src="https://github.com/user-attachments/assets/e08df1af-7c74-4196-82be-8b3a5172da23" />
<img width="976" height="542" alt="image" src="https://github.com/user-attachments/assets/56c99907-5cd5-4d54-8597-15ccaf8390fd" />

# Labs
        Create a Deployment
        Using the /root/deployment.yml manifest file provided , create a Kubernetes deployment for the Flask application.
        
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: flask-web-app
        spec:
          replicas: 2
          selector:
            matchLabels:
              app: flask-app
          template:
            metadata:
              labels:
                app: flask-app
            spec:
              containers:
              - name: flask
                image: rakshithraka/flask-web-app
                ports:
                - containerPort: 80
        ---
        apiVersion: v1
        kind: Service
        metadata:
          name: flask-web-app-service
        spec:
          type: ClusterIP
          selector:
            app: flask-app
          ports:
           - port: 80
             targetPort: 80   

             Manually scale the deployment named flask-web-app to have 3 replicas.
             k scale deploy  flask-web-app --replicas=3

             If you scale a deployment using kubectl scale to a higher number of replicas, 
             but the cluster has insufficient resources to accommodate all new replicas, what will happen?
             









