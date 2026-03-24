
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

<img width="747" height="362" alt="image" src="https://github.com/user-attachments/assets/4c54203e-bd70-4b89-9c72-7b39097f601d" />

<img width="912" height="357" alt="image" src="https://github.com/user-attachments/assets/e6ccb317-3966-4a32-b768-5b3b577cdf5d" />

<img width="742" height="537" alt="image" src="https://github.com/user-attachments/assets/55ddd360-e67f-43aa-9a0e-3d93716fcce0" />

<img width="872" height="376" alt="image" src="https://github.com/user-attachments/assets/39712b12-47f9-4665-b2d0-15d0c1d604a6" />

<img width="1071" height="557" alt="image" src="https://github.com/user-attachments/assets/622e5817-5ca2-41ae-b848-ac270b7928b8" />

<img width="1085" height="562" alt="image" src="https://github.com/user-attachments/assets/2b25af21-accf-4a7c-adca-25d8745ebf8f" />
