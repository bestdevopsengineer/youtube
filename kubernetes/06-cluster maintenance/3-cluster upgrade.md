<img width="957" height="478" alt="image" src="https://github.com/user-attachments/assets/aeba9146-0bd9-4631-9e4a-f5ae355d88ab" />

<img width="887" height="470" alt="image" src="https://github.com/user-attachments/assets/7cec5845-02d6-4117-a3c6-8c91a7b31024" />

# start with the master node
        kubeadm upgrade plan
        apt-get upgrade -y kubeadm=1.12.0-00
        kubeadm upgrade apply v1.12.0
        apt-get upgrade -y kubelet=1.12.0-00
        systemctl restart bubelet


<img width="702" height="452" alt="image" src="https://github.com/user-attachments/assets/f9a322e5-20ea-4a9a-abaa-a53fc2d5fce3" />
<img width="737" height="392" alt="image" src="https://github.com/user-attachments/assets/0b137da1-6c4d-49ce-9fc7-7a19abafb583" />

# update worker node
# 1st strategy with down time
<img width="748" height="543" alt="image" src="https://github.com/user-attachments/assets/a6fe0599-25fa-43f1-a98e-74021e6b506c" />
<img width="752" height="440" alt="image" src="https://github.com/user-attachments/assets/eb4c7434-27b5-42d1-80c4-7a46da7a22ca" />

# 2nd strategy (one node at the time)
        kubectl drain node-1
        apt-get upgrade -y kubeadm=1.12.0-00
        apt-get upgrade -y kubelet=1.12.0-00
        kubeadm upgrade node config --kubelet-version v1.12.0
        systemctl restart bubelet
        kubectl uncordon node-1

        kubectl drain node-2
        apt-get upgrade -y kubeadm=1.12.0-00
        apt-get upgrade -y kubelet=1.12.0-00
        kubeadm upgrade node config --kubelet-version v1.12.0
        systemctl restart bubelet
        kubectl uncordon node-2

        kubectl drain node-3
        apt-get upgrade -y kubeadm=1.12.0-00
        apt-get upgrade -y kubelet=1.12.0-00
        kubeadm upgrade node config --kubelet-version v1.12.0
        systemctl restart bubelet
        kubectl uncordon node-3
        
<img width="833" height="517" alt="image" src="https://github.com/user-attachments/assets/775a6ae8-f4e3-4a59-9d02-d24d36979450" />
<img width="847" height="531" alt="image" src="https://github.com/user-attachments/assets/0515a808-68f0-4160-aa04-3aae945023a5" />
<img width="731" height="451" alt="image" src="https://github.com/user-attachments/assets/8ef0fa4d-0b50-4a57-bafc-4cc377cfc2d5" />
<img width="858" height="440" alt="image" src="https://github.com/user-attachments/assets/d69bc7ed-1216-4a07-8e62-dd5106a31ab8" />

# 3rd startegy (add node with newer software version v1.11) cloud env
<img width="872" height="451" alt="image" src="https://github.com/user-attachments/assets/dda6d285-ff09-4b64-b575-0fdc286ab9bb" />
<img width="876" height="527" alt="image" src="https://github.com/user-attachments/assets/6813d416-789b-4324-a92b-4ea5e968dcab" />
<img width="725" height="452" alt="image" src="https://github.com/user-attachments/assets/1904f9ba-358b-4238-aa40-745673754d70" />
