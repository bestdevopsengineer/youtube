 # 0- pod.yaml:
                    apiVersion: v1
                    kind: Pod
                    
                    metadata:
                      name: nginx-pod
                      labels:
                        app: nginx-label
                    
                    spec:
                      containers:
                        - name: nginx-container
                          image: nginx


# 1- Replication Controller
                        apiVersion: v1
                        kind: ReplicationController
                        metadata:
                          name: nginx-pod
                          labels:
                            app: nginx-label
                        
                        spec:
                          replicas: 3
                          template:
                            metadata:
                              name: nginx-pod
                              labels:
                                app: nginx-label
    
                            spec:
                              containers:
                                - name: nginx-container
                                  image: nginx


# 2- ReplicaSet: can also manage pod not created by the replicaset that is why we add selector
                          apiVersion: v1
                          kind: ReplicaSet
                          metadata:
                            name: nginx-replicaset
                            labels:
                              app: nginx-rs-label
                          
                          spec:
                            replicas: 3
                            selector: 
                              matchLabels: 
                                app: nginx-rs-label
                            template:
                              metadata:
                                name: nginx-pod
                                labels:
                                  app: nginx-rs-label
                              
                              spec:
                                containers:
                                  - name: nginx-container
                                    image: nginx



             kubectl create -f rs.yaml
             kubectl scale --replicas=6 -f rs.yaml
             kubectl scale --replicas=6 replicaset nginx-replicaset
             kubectl delete replicaset nginx-replicaset
