[veldrane@jump ~]$ kubectl create ns simple-api
namespace/simple-api created

[veldrane@jump ~]$ kubens simple-api
Context "kubernetes-admin@kubernetes" modified.
Active namespace is "simple-api".

[veldrane@jump ~]$ kubectl create -f ./simple-api-pod.yaml 
pod/simple-api created

[veldrane@jump ~]$ kubectl get pods
NAME         READY   STATUS              RESTARTS   AGE
simple-api   0/1     ContainerCreating   0          5s
[veldrane@jump ~]$ kubectl get pods
NAME         READY   STATUS              RESTARTS   AGE
simple-api   0/1     ContainerCreating   0          6s
[veldrane@jump ~]$ kubectl get pods
NAME         READY   STATUS    RESTARTS   AGE
simple-api   1/1     Running   0          22s


[veldrane@jump ~]$ kubectl logs -f simple-api
2026-01-27 14:03:50.581943311 UTC ---| Info: Starting logger
2026-01-27 14:03:50.582983014 UTC ---| Info: Application initialized
2026-01-27 14:03:50.582994882 UTC ---| Info: Starting server on 0.0.0.0:8080
^C
[veldrane@jump ~]$ kubectl get pods -o wide
NAME         READY   STATUS    RESTARTS   AGE   IP          NODE                                    NOMINATED NODE   READINESS GATES
simple-api   1/1     Running   0          42s   10.38.2.9   wks-5325ab-00002.class.syscallx86.com   <none>           <none>


[veldrane@jump ~]$ curl http://10.38.2.9:8080 -v
*   Trying 10.38.2.9:8080...
