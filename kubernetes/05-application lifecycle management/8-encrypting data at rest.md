# Enabling Encryption at Rest for Secrets so they are stored encrypted in ETCD. 

        kubectl create secret generic my-secret --from-literal=key1=supersecret
        k describe secret my-secret
        k describe secret my-secret -o yaml
        echo "secret" | base64 --decode
        apt-get install etcd-client
        
        ETCDCTL_API=3 etcdctl \
          --cacert=/etc/kubernetes/pki/etcd/ca.crt \
          --cert=/etc/kubernetes/pki/etcd/server.crt \
          --key=/etc/kubernetes/pki/etcd/server.key \
          get /registry/secrets/default/my-secret | hexdump -C

          head -c 32 /dev/urandom | base64
          copy the result

          vi encryp.yaml:   #encrypt configuration file
          apiVersion: apiserver.config.k8s.io/v1
          kind: EncryptionConfiguration
          resources:
            - resources:
                - secrets
              providers:
                - aescbc:
                    keys:
                      - name: key1
                        secret: <BASE 64 ENCODED SECRET>   <--- paste the result
                - identity: {}

            mkdir /etc/kubernetes/enc
            mv encrypt.yaml /etc/kubernetes/enc
            vi /etc/kubernetes/manifests/kube-apiserver.yaml
            
            add line: --encryption-provider-config=/etc/kubernetes/enc/enc.yaml
            
            add volumemounts:
            - name: enc
              mountPath: /etc/kubernetes/enc
              readonly: true
            
            add volumes:
            - name: enc
              hostPath: 
                path: /etc/kubernetes/enc
                type: DirectoryOrCreate
            
            crictl pods
            kubectl create secret generic my-secret-2 --from-literal=key2=topsecret
            k get secret
            ETCDCTL_API=3 etcdctl \
            --cacert=/etc/kubernetes/pki/etcd/ca.crt \
            --cert=/etc/kubernetes/pki/etcd/server.crt \
            --key=/etc/kubernetes/pki/etcd/server.key \
            get /registry/secrets/default/my-secret-2 | hexdump -C

          you cant see the secret no more so encryption is enabled
