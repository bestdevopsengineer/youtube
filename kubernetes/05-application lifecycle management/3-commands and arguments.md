<img width="818" height="396" alt="image" src="https://github.com/user-attachments/assets/5d801ec8-ac38-4c6b-8a2c-f424066c4a00" />

<img width="928" height="432" alt="image" src="https://github.com/user-attachments/assets/5970447e-5b47-4da2-85b2-521ef23a7bea" />

# Labs

      Create a pod with the ubuntu image to run a container to sleep for 5000 seconds. Modify the file ubuntu-sleeper-2.yaml.
      apiVersion: v1 
      kind: Pod 
      metadata:
        name: ubuntu-sleeper-2 
      spec:
        containers:
        - name: ubuntu
          image: ubuntu
          command: ["sleep"]
          args: ["5000"]


          Create a pod using the file named ubuntu-sleeper-3.yaml
          apiVersion: v1 
          kind: Pod 
          metadata:
            name: ubuntu-sleeper-3 
          spec:
            containers:
            - name: ubuntu
              image: ubuntu
              command:
                - "sleep"
                - "1200"


              Update pod ubuntu-sleeper-3 to sleep for 2000 seconds.
              k edit ubuntu-sleeper-3.yaml
              k replace -f ubuntu-sleeper-3.yaml --force

              Dockerfile:
              FROM python:3.6-alpine
              RUN pip install flask
              COPY . /opt/
              EXPOSE 8080
              WORKDIR /opt
              ENTRYPOINT ["python", "app.py"]
              which command will be executed when a container is started from this image.: python app.py


              Dockerfile2:
              FROM python:3.6-alpine
              RUN pip install flask
              COPY . /opt/
              EXPOSE 8080
              WORKDIR /opt
              ENTRYPOINT ["python", "app.py"]
              CMD ["--color", "red"]
              which command will be executed when a container is started from this image.: python app.py --color red

              
