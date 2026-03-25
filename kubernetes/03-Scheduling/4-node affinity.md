           apiVersion: v1
          kind: Pod
          metadata:
            name: my-pod
          specs:
            containers:
            - name: nginx-container
              image: nginx
            NodeSelector:
              size: large
          
          two types of node affinity:
          
          # 🚨 REQUIRED: Pod will ONLY schedule on nodes that match these rules
          requiredDuringSchedulingIgnoredDuringExecution
          
           # ⭐ PREFERRED: Scheduler will TRY to place the Pod on these nodes
          preferredDuringSchedulingIgnoredDuringExecution
          
          
          apiVersion: v1
          kind: Pod
          metadata:
            name: affinity-demo
          spec:
            containers:
              - name: nginx
                image: nginx:latest
          
            affinity:
              nodeAffinity:
                requiredDuringSchedulingIgnoredDuringExecution:
                  nodeSelectorTerms:
                    - matchExpressions:
                        - key: size
                          operator: In
                          values:
                            - large
