<img width="1037" height="540" alt="image" src="https://github.com/user-attachments/assets/7a09cc84-814c-48c4-b537-39f5d207127a" />


              apiVersion: v1
              kind: ResourceQuota
              metadata:
                name: compute-quota
                namespace: dev
              spec:
                hard:
                  pods: "10"
                  requests.cpu: "4"
                  requests.memory: 5Gi
                  limits.cpu: "10"
                  limits.memory: 10Gi
