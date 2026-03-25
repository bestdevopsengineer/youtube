# what do you like to monitor:
      1- node level metrics 
        number of nodes
        how many are healthy
      2- performance metrics
        cpu
        memory
        network
        disk utilization
      3- pod level metric
        number of pods 
        performance metric of each pod (cpu,memory consumption on them)
        
# solution to monitor the metrics, store them, provide analytics around data
      prometheus
      metrics server
      elastic stack
      datadog
      dynatrace

<img width="332" height="482" alt="image" src="https://github.com/user-attachments/assets/f93b146e-a41f-489a-88e3-edb3a051269c" />

<img width="730" height="472" alt="image" src="https://github.com/user-attachments/assets/814311fd-9f07-4273-a608-4991dc07485e" />

<img width="642" height="408" alt="image" src="https://github.com/user-attachments/assets/0578cc6a-0aa8-4f56-ab1c-6b9d0b9cc123" />

# LABS
            Deploy the Metrics Server in your Kubernetes cluster by applying the latest release components.yaml manifest using the following command:
            Run the :
            kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
            kubectl top node
            NAME           CPU(cores)   CPU(%)   MEMORY(bytes)   MEMORY(%)   
            controlplane   175m         1%       893Mi           1%          
            node01         24m          0%       149Mi           0%    

            Identify the POD that consumes the least CPU(cores) in default namespace.
            root@controlplane:~# kubectl top pod --sort-by='cpu' --no-headers | tail -1 
            lion       2m     5Mi     
