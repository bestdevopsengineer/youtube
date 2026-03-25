    when creating a pod
    kubelet -> kube-apiserver -> create Pod -> etcd database
<img width="792" height="236" alt="image" src="https://github.com/user-attachments/assets/523a8801-1ac1-4609-bdad-be619fb938f2" />

    when the request hit the api-server:
    there is an authentication process
<img width="787" height="246" alt="image" src="https://github.com/user-attachments/assets/1467844a-838e-4039-a236-3d8cd42246dd" />

    done through certificate
    ./kube/config
    check if the user is valid
<img width="947" height="518" alt="image" src="https://github.com/user-attachments/assets/d3b49003-9478-48fe-a8a9-3bfe638de19a" />

    then the request go through an authorization process
    check if the user got permission to perform that operation
