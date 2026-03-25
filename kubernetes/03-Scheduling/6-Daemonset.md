Monitoring solution
Logs viewer


                apiVersion: apps/v1
                kind: DaemonSet
                metadata:
                  name: node-monitor
                  namespace: kube-system
                  labels:
                    app: node-monitor
                spec:
                  selector:
                    matchLabels:
                      app: node-monitor
                  template:
                    metadata:
                      labels:
                        app: node-monitor
                    spec:
                      containers:
                        - name: monitor-agent
                          image: busybox:latest
                          command: ["sh", "-c", "while true; do echo Monitoring node...; sleep 30; done"]



          Deploy a DaemonSet for FluentD Logging.
          Use the given specifications.
          Name: elasticsearch
          Namespace: kube-system
          Image: registry.k8s.io/fluentd-elasticsearch:1.20
                                    ---
          apiVersion: apps/v1
          kind: DaemonSet
          metadata:
            labels:
              app: elasticsearch
            name: elasticsearch
            namespace: kube-system
          spec:
            selector:
              matchLabels:
                app: elasticsearch
            template:
              metadata:
                labels:
                  app: elasticsearch
              spec:
                containers:
                - image: registry.k8s.io/fluentd-elasticsearch:1.20
                  name: fluentd-elasticsearch
