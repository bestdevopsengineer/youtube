
            when node goes down master wait for 5min (pod eviction time out set on controller manager tolerationSeconds: 3600)
            pod are terminated from that node
            if the pod recomes after 5min it comes blanc without any pod scheduled on it
            
            drain the node of all the workload
            pod will be terminated and recreated on another nodes
            kubectl drain node-1
            
            the node is marked as cordon
            mean no pod could be schedule on the node
            until we remove the restriction
            
            kubectl uncordon node-1
            
            if you do
            kubectl cordon node-2 
            it will make sure pod are not scheduled on the node

  # Labs
          We need to take node01 out for maintenance. Empty the node of all applications and mark it unschedulable.
          kubectl drain node01 --ignore-daemonsets
          Node node01 Unschedulable
          Pods evicted from node01

          The maintenance tasks have been completed. Configure the node node01 to be schedulable again.
          kubectl uncordon node01
          if you check node01 will not have pods only when new pods are created

          We need to carry out a maintenance activity on node01 again. 
          Try draining the node again using the same command as before: 
          kubectl drain node01 --ignore-daemonsets
          it will not work because 
          there is a single pod scheduled on node01 which is not part of a replicaset.
          The drain command will not work in this case. To forcefully drain the node we now have to use the --force flag.

          What would happen to hr-app if node01 is drained forcefully?
          A forceful drain of the node will delete any pod that is not part of a replicaset.

          Oops! We did not want to do that! hr-app is a critical application that should not be destroyed.
          We have now reverted back to the previous state and re-deployed hr-app as a deployment
          kubectl cordon node01
