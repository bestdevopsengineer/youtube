        taint -> node
        tolerate -> pod
        
        kubectl taint nodes node-name key=value:taint-effect-> what happen to pod that doesnt tolerate this taint
        
            taint-effect:
              1-NoSchedule -> pod will not be schedule on the node
              2-PreferNoSchedule -> system will try to avoid not placing the pod on the node
              3-NoExecute -> new pod will not be scheduled on the node


                apiVersion: v1
                kind: Pod
                metadata:
                  name: my-pod
                specs:
                  containers:
                  - name: nginx-container
                    image: nginx
                  tolerations:
                  - key: "app"
                    operator: "Equal"
                    value: "blue"
                    effect: "NoSchedule"

                kubectl taint nodes node01 app=blue:NoSchedule
                k taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-  -> remove the taint
