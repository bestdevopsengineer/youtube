<img width="755" height="441" alt="image" src="https://github.com/user-attachments/assets/a01847c4-ca4b-4b3c-961c-962805da500b" />

<img width="778" height="448" alt="image" src="https://github.com/user-attachments/assets/1748cc7a-970b-4084-940c-fdfbfa79c5f0" />

<img width="821" height="446" alt="image" src="https://github.com/user-attachments/assets/f775ee92-a1f6-407b-bdaf-1f26e328cc1f" />

<img width="822" height="481" alt="image" src="https://github.com/user-attachments/assets/6e2a93b8-3227-4618-b35b-813525cda3b7" />

<img width="1037" height="453" alt="image" src="https://github.com/user-attachments/assets/b699ed15-87dd-46b6-a25f-5eaec4633ffe" />

<img width="791" height="470" alt="image" src="https://github.com/user-attachments/assets/1ce3d0f6-4c3f-4eae-ac32-a7e4bcf07af8" />

<img width="867" height="462" alt="image" src="https://github.com/user-attachments/assets/d542571f-60df-4876-b551-42b2fa424bc6" />

# Labs
    1- how many secrets
        k get secrets
    2- how many secrets in dashboard-token
        k get secrets dashboard-token
    3- We are going to deploy an application with the below architecture
<img width="592" height="386" alt="image" src="https://github.com/user-attachments/assets/e2b4c0d2-5e0a-4b57-840d-3ffe006f6cd4" />

        We have already deployed the required pods and services. Check out the pods and services created. 
        Check out the web application using the Webapp MySQL link above your terminal, next to the Quiz Portal Link.

        Create a new secret named db-secret with the data given below. 
        DB_Host = sql01    DB_User = root   DB_Password = password123
        kubectl create secret generic db-secret \
        --from-literal=DB_Host=sql01 \
        --from-literal=DB_User=root \
        --from-literal=DB_Password=password123

        Configure the webapp-pod to load environment variables from the db-secret secret you created in the previous task.
        apiVersion: v1
        kind: Pod
        metadata:
          name: webapp-pod
          labels:
            name: webapp-pod
          namespace: default
        spec:
          containers:
          - name: webapp
            image: kodekloud/simple-webapp-mysql
            imagePullPolicy: Always
            envFrom:
            - secretRef:
                name: db-secret


            
