<img width="856" height="447" alt="image" src="https://github.com/user-attachments/assets/f0884999-c4ff-44d8-a296-4c9fe96581d5" />

<img width="905" height="473" alt="image" src="https://github.com/user-attachments/assets/eb1b52e6-af11-4f27-81a5-a97836b775c9" />

<img width="822" height="472" alt="image" src="https://github.com/user-attachments/assets/fd6e3f20-2112-4fc1-bd28-f09c21f2905a" />

<img width="745" height="442" alt="image" src="https://github.com/user-attachments/assets/cdb2005c-4429-4d56-acfa-ecf434d631c0" />

<img width="793" height="472" alt="image" src="https://github.com/user-attachments/assets/0a813c52-0e4a-4e10-87f0-7e5ab61b5ac6" />

# Labs
              ---
              apiVersion: v1
              kind: Pod
              metadata:
                labels:
                  name: webapp-color
                name: webapp-color
                namespace: default
              spec:
                containers:
                - env:
                  - name: APP_COLOR
                    value: green
                  image: kodekloud/webapp-color
                  name: webapp-color



                  Create a new ConfigMap for the webapp-color POD. Use the spec given below.
                  kubectl create configmap  webapp-config-map --from-literal=APP_COLOR=darkblue --from-literal=APP_OTHER=disregard

                  Update the environment variable on the POD to use only the APP_COLOR key from the newly created ConfigMap.
                  ---
                  apiVersion: v1
                  kind: Pod
                  metadata:
                    labels:
                      name: webapp-color
                    name: webapp-color
                    namespace: default
                  spec:
                    containers:
                    - env:
                      - name: APP_COLOR
                        valueFrom:
                         configMapKeyRef:
                           name: webapp-config-map
                           key: APP_COLOR
                      image: kodekloud/webapp-color
                      name: webapp-color


                      
