<img width="928" height="446" alt="image" src="https://github.com/user-attachments/assets/d0cbe408-a3d0-4ace-b66f-c275fc0a1d7c" />

# deploying an additional scheduler
<img width="807" height="287" alt="image" src="https://github.com/user-attachments/assets/45b2f937-94b9-4637-a5dc-9d3f111f7c39" />


      my-custom-scheduler.yaml:
      
      apiVersion: v1
      kind: Pod
      metadata:
        name: my-custom-scheduler
        namespace: kube-system
      spec:
        containers:
          - name: kube-scheduler
            image: k8s.gcr.io/kube-scheduler-amd64:v1.XX.X
            command:
              - kube-scheduler
              - --address=127.0.0.1
              - --kubeconfig=/etc/kubernetes/scheduler.conf
              - --config=/etc/kubernetes/my-scheduler-config.yaml



        my-scheduler-config.yaml:
        
        apiVersion: kubescheduler.config.k8s.io/v1
        kind: KubeSchedulerConfiguration
        profiles:
          - schedulerName: my-scheduler
            leaderElection:
              leaderElect: true
              resourceNamespace: kube-system
              resourceName: lock-object-my-scheduler
