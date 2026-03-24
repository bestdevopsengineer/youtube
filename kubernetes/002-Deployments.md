
                      apiVersion: v1
                      kind: Deployment
                      metadata:
                        name: nginx-deployment
                        labels:
                          app: nginx-deployment-label
                      
                      spec:
                        replicas: 3
                        selector: 
                          matchLabels: 
                            app: nginx-deployment-label
                        template:
                          metadata:
                            name: nginx-pod
                            labels:
                              app: nginx-deployment-label
                          
                          spec:
                            containers:
                              - name: nginx-container
                                image: nginx



         kubectl create -f rs.yaml
         kubectl scale --replicas=6 -f rs.yaml
         kubectl scale --replicas=6 replicaset nginx-replicaset
         kubectl delete replicaset nginx-replicaset
         kubectl get all
