<img width="1037" height="540" alt="image" src="https://github.com/user-attachments/assets/7a09cc84-814c-48c4-b537-39f5d207127a" />


                apiVersion: v1
                kind: ResourceQuota
                metadata:
                  name: compute-quota        # Name of the ResourceQuota object
                  namespace: dev             # Namespace where the quota applies
                
                spec:
                  hard:                      # Hard limits that cannot be exceeded
                    pods: "10"               # Max number of Pods allowed in this namespace
                    requests.cpu: "4"        # Total CPU requested by all Pods cannot exceed 4 cores
                    requests.memory: 5Gi     # Total memory requested cannot exceed 5Gi
                    limits.cpu: "10"         # Total CPU limits across all Pods cannot exceed 10 cores
                    limits.memory: 10Gi      # Total memory limits cannot exceed 10Gi
