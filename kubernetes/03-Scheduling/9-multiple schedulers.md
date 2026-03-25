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

<img width="870" height="507" alt="image" src="https://github.com/user-attachments/assets/f075de82-06c0-419e-b003-179dfe27c596" />

<img width="911" height="302" alt="image" src="https://github.com/user-attachments/assets/312e388f-0050-443e-ba00-7b0a79056cda" />

<img width="936" height="330" alt="image" src="https://github.com/user-attachments/assets/26343b41-1ca3-47b6-a169-ada040f85a39" />

# labs
            1- default scheduler
            kube-scheduler-controlplane 
            2- Image used to create it
             registry.k8s.io/kube-scheduler:v1.34.0
            3- We have already created the ServiceAccount and ClusterRoleBinding that our custom scheduler will make use of.
            kubectl get serviceaccount -n kube-system
            kubectl get clusterrolebinding

            4-Please create a ConfigMap that the new scheduler will utilize, implementing the concept of ConfigMap as a volume
            cat my-scheduler-configmap.yaml :
            
            apiVersion: v1
            data:
              my-scheduler-config.yaml: |
                apiVersion: kubescheduler.config.k8s.io/v1
                kind: KubeSchedulerConfiguration
                profiles:
                  - schedulerName: my-scheduler
                leaderElection:
                  leaderElect: false
            kind: ConfigMap
            metadata:
              creationTimestamp: null
              name: my-scheduler-config
              namespace: kube-system


              cat my-scheduler-config.yaml :
              
                  apiVersion: kubescheduler.config.k8s.io/v1
                  kind: KubeSchedulerConfiguration
                  profiles:
                    - schedulerName: my-scheduler
                  leaderElection:
                    leaderElect: false

            5- Deploy an additional scheduler to the cluster .
            cat my-scheduler.yaml :
            
            apiVersion: v1
            kind: Pod
            metadata:
              labels:
                run: my-scheduler
              name: my-scheduler
              namespace: kube-system
            spec:
              serviceAccountName: my-scheduler
              containers:
              - command:
                - /usr/local/bin/kube-scheduler
                - --config=/etc/kubernetes/my-scheduler/my-scheduler-config.yaml
                image: registry.k8s.io/kube-scheduler:v1.34.0
                livenessProbe:
                  httpGet:
                    path: /healthz
                    port: 10259
                    scheme: HTTPS
                  initialDelaySeconds: 15
                name: kube-second-scheduler
                readinessProbe:
                  httpGet:
                    path: /healthz
                    port: 10259
                    scheme: HTTPS
                resources:
                  requests:
                    cpu: '0.1'
                securityContext:
                  privileged: false
                volumeMounts:
                  - name: config-volume
                    mountPath: /etc/kubernetes/my-scheduler
              hostNetwork: false
              hostPID: false
              volumes:
                - name: config-volume
                  configMap:
                    name: my-scheduler-config


            6-Please modify the provided Pod manifest file located at /root/nginx-pod.yaml to specify that the Pod should be scheduled by your custom scheduler, which is named my-scheduler.
            cat nginx-pod.yaml :
            
            apiVersion: v1 
            kind: Pod 
            metadata:
              name: nginx 
            spec:
              schedulerName: my-scheduler
              containers:
              - image: nginx
                name: nginx

                
