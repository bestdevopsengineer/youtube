# rollout command
      1- kubectl rollout status deployment/myapp-deployment
      2- kubectl rollout history deployment/myapp-deployment

# 2 types of deployment strategies
      1- recreate
      2- rolling update
      
<img width="1122" height="322" alt="image" src="https://github.com/user-attachments/assets/477bd8f5-2af1-4477-b312-115f82424782" />

<img width="496" height="548" alt="image" src="https://github.com/user-attachments/assets/a74511ba-4651-49a1-b826-3be0e6ae6da7" />


      kubectl apply -f deploy.yaml
      rollout is triiger
      new version is created
      
      or 
      
      kubectl set image deployment/myapp-deployment nginx:1.9.1

<img width="1871" height="840" alt="image" src="https://github.com/user-attachments/assets/e0253b22-2882-437d-85f5-266c4dc5decf" />


# Upgrade
<img width="985" height="462" alt="image" src="https://github.com/user-attachments/assets/e9c39876-af84-46ee-a7ec-086b041a185d" />

<img width="992" height="462" alt="image" src="https://github.com/user-attachments/assets/56821310-78dc-42ee-8237-ab8346be11e7" />

<img width="1030" height="521" alt="image" src="https://github.com/user-attachments/assets/1bded66b-7555-4d73-84b9-4430dd8cd199" />

<img width="907" height="535" alt="image" src="https://github.com/user-attachments/assets/d1ff51b0-7fde-42ab-9e3b-d6a5454b995e" />

# Labs
            kodekloud/webapp-color:v1
            k set image deployment/frontend simple-webapp=kodekloud/webapp-color:v2
            Recreate
             k set image deployment/frontend simple-webapp=kodekloud/webapp-color:v3
