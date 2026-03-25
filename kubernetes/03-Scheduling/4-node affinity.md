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
