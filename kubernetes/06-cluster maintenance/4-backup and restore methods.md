
# backup resources config: (best for managed cluster)

        kubectl get all --allnamespaces -o yaml > all-deployed-services.yaml

        tool like Velero can help to :
        Backing up Kubernetes resources (YAML objects)
        Backing up persistent volumes (via snapshots or Restic)
        Restoring clusters or namespaces
        Migrating workloads between clusters

# backup etcd:
        --data-dir=/var/lib/etcd
        take a snapshot
        etcdctl snapshot save snapshot.db \
        --endpoints=https://127.0.0.1:2379 \
        --cacert=/etc/etcd/ca.crt \
        --cert=/etc/etcd/etcd.server.crt \
        --key=/etc/etcd/etcd-server.key
        
        etcdctl snapshot status sanpshot.db
        systemctl stop kube-apiserver
        etcdctl snapshot restore snapshot.b --data-dir /var/lib/etcd-from-backup
        systemctl daemon-reload
        systemctl restart etcd
        systemc start kube-apiserver

# Working with ETCDCTL and ETCDUTL
      To make use of etcdctl for tasks such as backup, verify it is running on API version 3.x:
      etcdctl version
      
        Backing Up ETCD To take a snapshot from a running etcd server, use:
        ETCDCTL_API=3 etcdctl \
          --endpoints=https://127.0.0.1:2379 \
          --cacert=/etc/kubernetes/pki/etcd/ca.crt \
          --cert=/etc/kubernetes/pki/etcd/server.crt \
          --key=/etc/kubernetes/pki/etcd/server.key \
          snapshot save /backup/etcd-snapshot.db
       


          Using etcdutl (File-based Backup):
          etcdutl backup \
          --data-dir /var/lib/etcd \
          --backup-dir /backup/etcd-backup

          You can inspect the metadata of a snapshot file using:
          etcdctl snapshot status /backup/etcd-snapshot.db \
          --write-out=table

          Restoring ETCD Using etcdutl:
          etcdutl snapshot restore /backup/etcd-snapshot.db \
          --data-dir /var/lib/etcd-restored

          Notes:
          etcdctl snapshot save: is used for creating .db snapshots from live etcd clusters.
          etcdctl snapshot status: provides metadata information about the snapshot file.
          etcdutl snapshot restore: is used to restore a .db snapshot file.
          etcdutl backup : performs a raw file-level copy of etcd’s data and WAL files without                   needing etcd to be running.
          
        
# Labs:


        1-What is the version of ETCD running on the cluster?Check the ETCD Pod or Process 
        kubectl describe pod etcd-controlplane  -n kube-system
        Image:         registry.k8s.io/etcd:3.6.4-0

        2-At what address can you reach the ETCD cluster from the controlplane node?
        kubectl describe pod etcd-controlplane -n kube-system
        check for --listen-client-urls

        3-Where is the ETCD server certificate file located?
        kubectl -n kube-system describe pod etcd-controlplane | grep '\--cert-file'

        4-Where is the ETCD CA Certificate file located?
        kubectl -n kube-system describe pod etcd-controlplane | grep '\--trusted-ca-file'

        5-Take a snapshot of the ETCD database using the built-in snapshot functionality. 
        Store the backup file at location /opt/snapshot-pre-boot.db
        ETCDCTL_API=3 etcdctl \
          --endpoints=https://127.0.0.1:2379 \
          --cacert=/etc/kubernetes/pki/etcd/ca.crt \
          --cert=/etc/kubernetes/pki/etcd/server.crt \
          --key=/etc/kubernetes/pki/etcd/server.key \
          snapshot save /opt/snapshot-pre-boot.db

        6- check we lost everything

        7-Restore the original state of the cluster using the backup file.
        Step 1: Stop the kube-apiserver
        mv /etc/kubernetes/manifests/kube-apiserver.yaml /tmp/
        sleep 30

        Step 2: Restore the etcd snapshot
        etcdutl snapshot restore /opt/snapshot-pre-boot.db --data-dir /var/lib/etcd-from-backup

        Step 3: Update the etcd configuration
        vi /etc/kubernetes/manifests/etcd.yaml
        
        Modify the volumes section as follows:
        FROM
          volumes:
          - hostPath:
              path: /etc/kubernetes/pki/etcd
              type: DirectoryOrCreate
            name: etcd-certs
          - hostPath:
              path: /var/lib/etcd                    # OLD directory
              type: DirectoryOrCreate
            name: etcd-data
        TO:
          volumes:
          - hostPath:
              path: /etc/kubernetes/pki/etcd
              type: DirectoryOrCreate
            name: etcd-certs
          - hostPath:
              path: /var/lib/etcd-from-backup        # NEW restored directory
              type: DirectoryOrCreate
            name: etcd-data

        Step 4: Restart the kube-apiserver
        mv /tmp/kube-apiserver.yaml /etc/kubernetes/manifests/

        Step 5: Restart other control plane components
        # Restart kube-controller-manager
        mv /etc/kubernetes/manifests/kube-controller-manager.yaml /tmp/
        sleep 20
        mv /tmp/kube-controller-manager.yaml /etc/kubernetes/manifests/
        
        # Restart kube-scheduler
        mv /etc/kubernetes/manifests/kube-scheduler.yaml /tmp/
        sleep 20
        mv /tmp/kube-scheduler.yaml /etc/kubernetes/manifests/
        
        # Restart kubelet
        systemctl restart kubelet

        Step 6: Monitor the restart process
        watch crictl ps

        Step 7: Verify the restore
        # Check all resources across all namespaces
        kubectl get deployments,services --all-namespaces
        
        # Verify specific resources if needed
        kubectl get pods --all-namespaces
        kubectl get nodes
        
