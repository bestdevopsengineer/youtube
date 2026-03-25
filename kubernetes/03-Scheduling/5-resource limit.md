
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
specs:
  containers:
  - name: nginx-container
    image: nginx
    ports:
      - containerPort: 8080
    resources:
      requests:
        memory: "4Gi"
        cpu: 2
      limits:
        memory: "6Gi"
        cpu: 2


containers can not use more cpu than its limits

containers can use more memory than its limits (pod will be terminated OOM)



            Limit range (pod/container Level): default value to be set for containers in the pods
            if you create or update limit range it doesnt affect older pods
            
            apiVersion: v1
            kind: LimitRange
            metadata:
              name: resource-limits
              namespace: dev
            spec:
              limits:
                - type: Container
                  max:
                    cpu: "2"
                    memory: "2Gi"
                  min:
                    cpu: "100m"
                    memory: "128Mi"
                  default:
                    cpu: "500m"
                    memory: "512Mi"
                  defaultRequest:
                    cpu: "250m"
                    memory: "256Mi"
                  maxLimitRequestRatio:
                    cpu: "4"


          Resource Quota (NameSpace Level):
          apiVersion: v1
          kind: ResourceQuota
          metadata:
            name: compute-quota
          spec:
            hard:
              pods: "20"                 # Max number of Pods in this namespace
              requests.cpu: "4"          # Total CPU requests cannot exceed 4 cores
              requests.memory: 8Gi       # Total memory requests cannot exceed 8Gi
              limits.cpu: "10"           # Total CPU limits cannot exceed 10 cores
              limits.memory: 16Gi        # Total memory limits cannot exceed 16Gi
              configmaps: "10"           # Max number of ConfigMaps
              secrets: "20"              # Max number of Secrets
              persistentvolumeclaims: "5" # Max number of PVCs
