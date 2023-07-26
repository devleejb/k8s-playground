# simple-example-with-spring-boot

ReplicationController를 이용하여 쿠버네티스에서 간단한 SpringBoot 애플리케이션을 동작시키는 예제입니다.

Template을 이용하여 Replica를 하나 생성하고, NodePort Service를 이용하여 해당 Pod에 접근합니다.

## How to run

1. Kubectl을 이용하여 `replication.yaml` 적용
   ```sh
   kubectl apply -f replication.yaml
   ```
2. Pod의 상태가 Ready가 될 때까지 대기
   ```sh
   # Check status of pod
   kubectl describe pod
   ```
   결과 예시
   ```sh
    Type    Reason     Age   From               Message
    ----    ------     ----  ----               -------
    Normal  Scheduled  14m   default-scheduler  Successfully assigned default/simple-example-with-spring-boot-sx9w8 to minikube
    Normal  Pulling    14m   kubelet            Pulling image "jongbeomlee/simple-spring-boot"
    Normal  Pulled     14m   kubelet            Successfully pulled image "jongbeomlee/simple-spring-boot" in 2.012199459s (2.012211542s including waiting)
    Normal  Created    14m   kubelet            Created container spring-boot
    Normal  Started    14m   kubelet            Started container spring-boot
   ```

## How to check result

1. `minikube service` 명령어를 통해서 해당 서비스를 접근 가능하도록 함

   ```sh
   minikube service spring-boot-service
   ```

   결과 예시

   ```sh
   |-----------|---------------------|-------------|---------------------------|
   | NAMESPACE |        NAME         | TARGET PORT |            URL            |
   |-----------|---------------------|-------------|---------------------------|
   | default   | spring-boot-service |        8080 | http://192.168.49.2:30000 |
   |-----------|---------------------|-------------|---------------------------|
   🏃  Starting tunnel for service spring-boot-service.
   |-----------|---------------------|-------------|------------------------|
   | NAMESPACE |        NAME         | TARGET PORT |          URL           |
   |-----------|---------------------|-------------|------------------------|
   | default   | spring-boot-service |             | http://127.0.0.1:49381 |
   |-----------|---------------------|-------------|------------------------|
   🎉  Opening service default/spring-boot-service in default browser...
   ❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.
   ```
