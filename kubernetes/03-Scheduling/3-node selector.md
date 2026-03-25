
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



      kubectl label nodes <node-name> <label-key=label-value>
      kubectl label nodes node01 size=large
      kubectl create -f pod.yaml
    
