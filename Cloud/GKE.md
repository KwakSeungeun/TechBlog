### 실습 코드 Github 주소

```git clone https://github.com/googlecodelabs/orchestrate-with-kubernetes.git```

* 🐤monolith type(1 container) yaml files
    ```
    apiVersion: v1
    kind: Pod
    metadata:
    name: monolith
    labels:
        app: monolith
    spec:
    containers:
        - name: monolith
        image: kelseyhightower/monolith:1.0.0
        args:
            - "-http=0.0.0.0:80"
            - "-health=0.0.0.0:81"
            - "-secret=secret"
        ports:
            - name: http
            containerPort: 80
            - name: health
            containerPort: 81
        resources:
            limits:
            cpu: 0.2
            memory: "10Mi"
    ```
    * pod은 1개의 container로 구성되어 있음
    * port는 80포이 개방

* 위의 yaml file을 사용하여 pod생성
    ``` 
    kubectl create -f pods/monolith.yaml
    ```

* ``` kubectl describe pods [pod이름] ``` 에서 나오는 정보들이 yaml파일에 적어둔 것

* pod과의 통신 
    
    pod은 kubernetes내부에서 동작하므로 외부로 노출되는 IP가 없다. 따라서 ```kubectl port-forward monolith 10080:80``` 명령어를 사용해 local port를 pod 안의 포트로 mapping한다. (위의 설정에서 pod은 80 port가 오픈되어 있으므로 이와 local의 10080 port를 연결한다)

* pod의 로그 확인 ```kubectl logs [pod이름]```

    -f option을 추가하면 계속해서 log를 monitoring 할 수 있다

* ```kubectl exec``` 명령어를 사용하여 모놀리식 pod의 대화형 셸을 실행. 이는 컨테이너 내부에서 문제를 해결할 때 유용하다. 끝내기 :  ```exit```

* 서비스는 라벨을 사용하여 어떤 pod에서 작동할지 결정합니다. pod에 라벨이 정확히 지정되어 있다면 서비스가 이를 자동으로 감지하고 노출시킵니다.

* 서비스가 제공하는 pod 집합에 대한 액세스 수준은 서비스 유형에 따라 다릅니다. 현재 3가지 유형이 있습니다.

    * ClusterIP(내부) -- 기본 유형이며 이 서비스는 클러스터 안에서만 볼 수 있습니다.
    * NodePort 클러스터의 각 노드에 외부에서 액세스 가능한 IP 주소를 제공합니다.
    * LoadBalancer는 클라우드 제공업체로부터 부하 분산기를 추가하며 서비스에서 유입되는 트래픽을 내부에 있는 노드로 전달합니다.


* service의 selector에서 연결될 pod를 지정하게 되는데 이는 label로 지정이 된다!
