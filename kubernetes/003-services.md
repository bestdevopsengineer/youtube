
            apiVersion: v1
            kind: Services
            metadata:
              name: nginx-svc
              labels:
                app: nginx-svc-label
            
            spec:
              type: NodePort
              ports:
                - targetPort: 80
                  port: 80
                  nodePort: 300008

<img width="1020" height="347" alt="image" src="https://github.com/user-attachments/assets/242ff86d-c2a1-4faa-9ca9-89a0dc8a8866" />

<img width="875" height="378" alt="image" src="https://github.com/user-attachments/assets/6f5e79c3-04cc-47f3-8398-53fb2452781e" />
