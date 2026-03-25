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

    then the request go through an authorization process (RBAC)
    check if the user got permission to perform that operation
<img width="1038" height="455" alt="image" src="https://github.com/user-attachments/assets/75e58f62-0c1e-4d7f-988c-703a6a932865" />

<img width="847" height="318" alt="image" src="https://github.com/user-attachments/assets/64a66bc6-4e3e-4328-9fa7-066c743c6df2" />

<img width="848" height="465" alt="image" src="https://github.com/user-attachments/assets/1bf4d6e6-b583-4ff2-8a01-0daef8e60685" />

<img width="848" height="465" alt="image" src="https://github.com/user-attachments/assets/e06c20d4-5d70-4a39-a532-6d29dbd413ca" />

<img width="1823" height="641" alt="image" src="https://github.com/user-attachments/assets/53bff9b8-ccc6-4d98-9a7e-e5e6f7a48031" />

# Admission Controllers Enable by default

<img width="1525" height="492" alt="image" src="https://github.com/user-attachments/assets/b80cb245-2abd-433b-beee-e3f58d9ccd00" />

# enable NamespaceAutoProvision so that pod will get create even if the namespace is not created before

<img width="1711" height="487" alt="image" src="https://github.com/user-attachments/assets/bc411f8d-9fd6-4fbc-8316-e0beaa703470" />

<img width="1780" height="846" alt="image" src="https://github.com/user-attachments/assets/923840d8-9524-4f04-a110-f5b2e0499ba5" />

# LABS

    The ImagePolicyWebhook admission controller intercepts pod creation requests and consults an external webhook service 
    to determine whether the container images specified in the pod spec should be allowed or denied.
    In this lab, you will configure an ImagePolicyWebhook admission controller to work with a container image scanner.
    A functional container image scanner is already deployed with the HTTPS endpoint:
    https://image-checker-webhook.default.svc:1323/image_policy
    An incomplete configuration exists at /etc/kubernetes/imgvalidation.

    1-What is the primary purpose of the ImagePolicyWebhook admission controller?
    The ImagePolicyWebhook admission controller intercepts pod creation and update requests, 
    extracts the container images, and sends them to an external webhook for validation. 
    Based on the webhook's response, it either allows or denies the pod creation.

    2-








