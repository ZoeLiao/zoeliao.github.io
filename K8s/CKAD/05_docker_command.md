# Docker Command
- Use "arg" (CMD) and "command" (ENTRYPOINT)in Pod
    - ```Dockerfile
      FROM Ubuntu
      ENTRYPOINT ["sleep"]
      CMD ["3"]
      ```
    - ```yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: app-pod
      spec:
        containers:
          - name: app-pod
            image: app
            command: ["echo"] <-- replace "sleep"
            args: ["5"] <-- replace "3"
      ```
