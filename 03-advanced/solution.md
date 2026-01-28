#### Final deployment, configmap and service






```cm-simple-api.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: simple-api-config
data:
  config.yaml: |
    "addr" : "0.0.0.0"
    "port" : 8080
    "prefix" : "/api/v1"
    "log": "console"
    "fault_inject":
      "error_rate": 0.3
      "min_delay": 50
      "max_delay": 500
      "timeout": 150
      "status_code": 500
```

```de-simple-api.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    template: simple-api
  name: simple-api
spec:
  selector:
    matchLabels:
      app: simple-api
  template:
    metadata:
      annotations:
        prometheus.io/scrape: "true"
      creationTimestamp: null
      labels:
        app: simple-api
      name: simple-api
    spec:
      containers:
      - args:
        - -c
        - /etc/simple/config.yaml
        env:
        - name: TZ
          value: Europe/Prague
        image: registry.class.syscallx86.com/simple-api:v1.1.0
        imagePullPolicy: Always
        name: simple-api
        ports:
          - name: http
            containerPort: 8080
            protocol: TCP
        resources:
          limits:
            cpu: 100m
            memory: 200M
          requests:
            cpu: 100m
            memory: 200M
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /etc/simple/config.yaml
          name: simple-api-config
          subPath: config.yaml
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext:
        runAsNonRoot: true
        runAsUser: 10001
      terminationGracePeriodSeconds: 30
      volumes:
      - configMap:
          defaultMode: 420
          items:
          - key: config.yaml
            path: config.yaml
          name: simple-api-config
        name: simple-api-config
```