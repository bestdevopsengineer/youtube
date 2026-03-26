# k get pods
      NAME     READY   STATUS    RESTARTS   AGE
      webapp   1/1     Running   0          24s

      kubectl exec webapp -- cat /log/app.log
      if we delete the pod we will not see those logs no more

# Configure a volume to store these logs at /var/log/webapp on the host.
            kubectl delete po webapp
            
            apiVersion: v1
            kind: Pod
            metadata:
              name: webapp
            spec:
              containers:
              - name: event-simulator
                image: kodekloud/event-simulator
                env:
                - name: LOG_HANDLERS
                  value: file
                volumeMounts:
                - mountPath: /log
                  name: log-volume
            
              volumes:
              - name: log-volume
                hostPath:
                  # directory location on host
                  path: /var/log/webapp
                  # this field is optional
                  type: Directory

  # Create a Persistent Volume with the given specification.
            apiVersion: v1
            kind: PersistentVolume
            metadata:
              name: pv-log
            spec:
              persistentVolumeReclaimPolicy: Retain
              accessModes:
                - ReadWriteMany
              capacity:
                storage: 100Mi
              hostPath:
                path: /pv/log

  # Create a Persistent Volume Claim with the given specification.
            kind: PersistentVolumeClaim
            apiVersion: v1
            metadata:
              name: claim-log-1
            spec:
              accessModes:
                - ReadWriteOnce
              resources:
                requests:
                  storage: 50Mi

    # why pvc is pending
          access mode mismatch
          Update the Access Mode on the claim to bind it to the PV.
          
          kind: PersistentVolumeClaim
            apiVersion: v1
            metadata:
              name: claim-log-1
            spec:
              accessModes:
                - ReadWriteMany
              resources:
                requests:
                  storage: 50Mi

    # Update the webapp pod to use the persistent volume claim as its storage.
              apiVersion: v1
              kind: Pod
              metadata:
                name: webapp
              spec:
                containers:
                - name: event-simulator
                  image: kodekloud/event-simulator
                  env:
                  - name: LOG_HANDLERS
                    value: file
                  volumeMounts:
                  - mountPath: /log
                    name: log-volume
              
                volumes:
                - name: log-volume
                  persistentVolumeClaim:
                    claimName: claim-log-1

      # What would happen to the PV if the PVC was destroyed?
                persistentVolumeReclaimPolicy: Retain for pv 
                pv will not delete but unaivalable
                I tried to delete pvc but it stocked
                
