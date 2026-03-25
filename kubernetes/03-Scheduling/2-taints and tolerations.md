        taint -> node
        tolerate -> pod
        
        kubectl taint nodes node-name key=value:taint-effect-> what happen to pod that doesnt tolerate this taint
        
            taint-effect:
              1-NoSchedule -> pod will not be schedule on the node
              2-PreferNoSchedule -> system will try to avoid not placing the pod on the node
              3-NoExecute -> new pod will not be scheduled on the node
