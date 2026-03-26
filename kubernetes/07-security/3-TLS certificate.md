<img width="813" height="331" alt="image" src="https://github.com/user-attachments/assets/06cad105-b0dd-4cd4-925f-a94479f12cff" />

<img width="612" height="382" alt="image" src="https://github.com/user-attachments/assets/b32121b7-5ceb-44c0-bf7c-bebb6e7adc58" />

<img width="880" height="447" alt="image" src="https://github.com/user-attachments/assets/0d3db29c-df22-4471-addc-2cb78dbda3b6" />

<img width="860" height="485" alt="image" src="https://github.com/user-attachments/assets/39ea21c5-1f1c-4b89-add4-989610ff347a" />

<img width="682" height="477" alt="image" src="https://github.com/user-attachments/assets/fa7dccbe-2635-4251-8492-cbbec55deb74" />

# certificate creation tools
<img width="602" height="153" alt="image" src="https://github.com/user-attachments/assets/9225c17e-3211-474c-80d2-55124d567576" />

<img width="887" height="332" alt="image" src="https://github.com/user-attachments/assets/a9f388a4-4af9-48cc-a51f-df13dabf0f02" />

<img width="852" height="366" alt="image" src="https://github.com/user-attachments/assets/313ce744-7025-4fc2-a30e-d80ade8d8964" />

# labs
      1-Identify the certificate file used for the kube-api server.
      cat /etc/kubernetes/manifests/kube-apiserver.yaml
      - --tls-cert-file=/etc/kubernetes/pki/apiserver.crt

      2-Identify the Certificate file used to authenticate kube-apiserver as a client to ETCD Server.
      cat /etc/kubernetes/manifests/kube-apiserver.yaml
      - --etcd-certfile=/etc/kubernetes/pki/apiserver-etcd-client.crt

      3-Identify the key used to authenticate kubeapi-server to the kubelet server.
      cat /etc/kubernetes/manifests/kube-apiserver.yaml
      - --kubelet-client-key=/etc/kubernetes/pki/apiserver-kubelet-client.key

      4-Identify the ETCD Server Certificate used to host ETCD server.
      cat /etc/kubernetes/manifests/etcd.yaml
      - --cert-file=/etc/kubernetes/pki/etcd/server.crt

      5-Identify the ETCD Server CA Root Certificate used to serve ETCD Server
      cat /etc/kubernetes/manifests/etcd.yaml
      - --peer-trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt

      6-What is the Common Name (CN) configured on the Kube API Server Certificate?
      openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
      Subject: CN = kube-apiserver

      7-What is the name of the CA who issued the Kube API Server Certificate?
      openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
      Issuer: CN = kubernetes

      8-What is the Common Name (CN) configured on the ETCD Server certificate?
      openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text
      Subject: CN = controlplane

      9-How long, from the issued date, is the Kube-API Server Certificate valid for?
      openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text
      Validity
            Not Before: Mar 26 07:44:48 2026 GMT
            Not After : Mar 26 07:49:48 2027 GMT

      10-How long, from the issued date, is the Root CA Certificate valid for?
      openssl x509 -in /etc/kubernetes/pki/ca.crt -text
      Validity
            Not Before: Mar 26 07:44:48 2026 GMT
            Not After : Mar 23 07:49:48 2036 GMT

      11-Kubectl suddenly stops responding to your commands. 
      Check it out! Someone recently modified the /etc/kubernetes/manifests/etcd.yaml file

      12-The kube-api server stopped again! Check it out. Inspect the kube-api server logs and identify the root cause and fix the issue.
      crictl ps -a | grep kube-apiserver
      
      
      
