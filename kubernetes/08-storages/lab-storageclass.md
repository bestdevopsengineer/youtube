# 1-how many storage class
       k get sc
      NAME                   PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
      local-path (default)   rancher.io/local-path   Delete          WaitForFirstConsumer   false                  2m39s

# 2-How many Storage Classes exist in the cluster?
      k get sc
      NAME                        PROVISIONER                     RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
      local-path (default)        rancher.io/local-path           Delete          WaitForFirstConsumer   false                  3m55s
      local-storage               kubernetes.io/no-provisioner    Delete          WaitForFirstConsumer   false                  70s
      portworx-io-priority-high   kubernetes.io/portworx-volume   Delete          Immediate              false                  70s


# 3-What is the name of the Storage Class that does not support dynamic volume provisioning?
      local-storage               kubernetes.io/no-provisioner    Delete          WaitForFirstConsumer   false                  70s

# 4-What is the Volume Binding Mode used for this storage class (the one identified in the previous question)?
      WaitForFirstConsumer

# 5-What is the Provisioner used for the storage class called portworx-io-priority-high?
      portworx-volume

# 6-Create a new PersistentVolumeClaim named local-pvc with the following configuration:

          StorageClass: local-path
          Access Mode: ReadWriteOnce
          Requested Storage: 500Mi
          Do not use the volumeName field in the PVC.

              apiVersion: v1
              kind: PersistentVolumeClaim 
              metadata:
                name: local-pvc
              spec:
                accessModes: 
                  - ReadWriteOnce
                resources:
                  requests: 
                    storage: 500Mi
                storageClassName: local-path

          
# 7-Why is the PVC still in a pending state, even though it includes a valid request using the local-path storage class?
              waiting a pod that will consume it

# 8-
