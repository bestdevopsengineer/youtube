          Help to define priorities for different workloads 
          so higher priority workload always get priority
          over lower priority ones.

                                          2 000 000 000
          kubernetes components   system  
                                          1 000 000 000
          databases               app      
          critical apps           app
          jobs                    app
          
                                          -2 147 483 648



          kubectl get priorityclass

          apiVersion: scheduling.k8s.io/v1
          kind: PriorityClass
          metadata:
            name: high-priority                   ########
          value: 1000000000
          description: "This priority class is used for high‑priority workloads."
          globalDefault: false

          associate this priority class to a pod 

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
                  ports:
                    - containerPort: 8080
              priorityClassName: high-priority      #######



              if you dont define a priority for a pod the default is 0
              If globalDefault:true, Pods without a priority automatically get this one


# effect of pod priority
                    critical apps  7   7   7
                    jobs           5   5   5

                    if we have high priority job coming 
                                    6   6   6
                    from prermptionPolicy:
                    we will know what to do
                    if not set default= PreemptLowerPriority
                    that mean kill lower job and take their place
                    critical apps  7   7   7
                     high priority 6   6   6

                     you can set it to never , so they will not get kill
