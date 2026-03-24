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


# 2- ReplicaSet
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
                                  app: nginx-label
                              
                              spec:
                                containers:
                                  - name: nginx-container
                                    image: nginx
