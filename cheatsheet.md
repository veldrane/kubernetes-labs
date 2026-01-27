### Příklady příkazů

#### Obecné

- ziskej token pro kubernetes dashboard
```bash
$ token
eyJhbGciOiJSUzI1NiIsImtpZCI6ImxMS3BMOVIxRVVpam5OVGtWVlEwY2tNQzVOVmhsRTFzYmZqcWJQVWtsakkifQ.eyJhdWQiOlsiaHR0cHM6Ly9rdWJlcm5ldGVzLmRlZmF1bHQuc3ZjLmNsdXN0ZXIubG9jYWwiXSwiZXhwIjoxNzY5NTIzMzE3LCJpYXQiOjE3Njk1MTk3MTcsImlzcyI6Imh0dHBzOi8va3ViZXJuZXRlcy5kZWZhdWx0LnN2Yy5jbHVzdGVyLmxvY2FsIiwianRpIjoiYjk4MDNlOGYtNzkxZS00NWNiLTk2YzktZGFmZjc5OGE5NGRiIiwia3ViZXJuZXRlcy5pbyI6eyJuYW1lc3BhY2UiOiJkYXNoYm9hcmQiLCJzZXJ2aWNlYWNjb3VudCI6eyJuYW1lIjoiZGFzaGJvYXJkLWFkbWluIiwidWlkIjoiODlhNTRjYmUtYmQwMS00YTU2LThiYmUtYTA4ZTI3MGY2MzgzIn19LCJuYmYiOjE3Njk1MTk3MTcsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkYXNoYm9hcmQ6ZGFzaGJvYXJkLWFkbWluIn0.Idq1m_RcAH2nF0UpDg0NnGA5-iX8RvBC4rSNq1dfUaMjpLgqgqm9ensdJ0Ae4ydcyJtD3XB0YpQvhKcFjblfriXGgUt7YmfvKKj_7gv9BrXAyEvUVlskk5HA3WSLWrYfH9B6OWFHlL-qDo5D3zInVeAq4U5ALd-fMa5A1QuDpzn1hjhNQSA-XrOLUsi2VCZ7yQT-Qb4MuGL1ekVUHXu2aV410--vZ71aRBsnVnivnkcvowTI3RK9I88pZhxE0mOkeKsN9-i1kkrazJdhM_rUbSh8CbScY49zL1v6aQulzaGhO8GzzMhHknc2NneuIU6tCB9wbcS7NOEkSHYfxs8Jfw
```

- přepni se do namespacu dashboard
```bash
$ kubens dashboard
Context "kubernetes-admin@kubernetes" modified.
Active namespace is "dashboard".
```


#### Pod management

- vypiš pody v ns
```bash
# kubectl get pods -n dashboard
NAME                                                  READY   STATUS    RESTARTS   AGE
kubernetes-dashboard-api-64bbbb48b-b8vjj              1/1     Running   0          36m
kubernetes-dashboard-auth-579765ddf4-j46bj            1/1     Running   0          36m
kubernetes-dashboard-kong-76c74d5846-gvqlh            1/1     Running   0          36m
kubernetes-dashboard-metrics-scraper-db57c765-ww28w   1/1     Running   0          36m
kubernetes-dashboard-web-dcc99865c-blrnd              1/1     Running   0          36m
```

- vypiš pody v ns i s detaily
```bash 
# kubectl get nodes -o wide
NAME                                    STATUS   ROLES           AGE     VERSION    INTERNAL-IP   EXTERNAL-IP   OS-IMAGE                      KERNEL-VERSION                 CONTAINER-RUNTIME
ctl-5325ab-00001.class.syscallx86.com   Ready    control-plane   2d21h   v1.30.14   10.4.1.11     <none>        Rocky Linux 9.7 (Blue Onyx)   5.14.0-611.24.1.el9_7.x86_64   cri-o://1.30.10
wks-5325ab-00001.class.syscallx86.com   Ready    worker          2d21h   v1.30.14   10.4.1.81     <none>        Rocky Linux 9.7 (Blue Onyx)   5.14.0-611.24.1.el9_7.x86_64   cri-o://1.30.10
wks-5325ab-00002.class.syscallx86.com   Ready    worker          2d21h   v1.30.14   10.4.1.82     <none>        Rocky Linux 9.7 (Blue Onyx)   5.14.0-611.24.1.el9_7.x86_64   cri-o://1.30.10
```

- vypiš detaily ke konkrétnímu pod
```bash
$ kubectl describe pod kubernetes-dashboard-api-64bbbb48b-b8vjj
Name:             kubernetes-dashboard-api-64bbbb48b-b8vjj
Namespace:        dashboard
Priority:         0
Service Account:  kubernetes-dashboard-api
Node:             wks-5325ab-00001.class.syscallx86.com/10.4.1.81
Start Time:       Tue, 27 Jan 2026 13:34:35 +0100
Labels:           app.kubernetes.io/component=api
                  app.kubernetes.io/instance=kubernetes-dashboard
                  app.kubernetes.io/managed-by=Helm
                  app.kubernetes.io/name=kubernetes-dashboard-api
                  app.kubernetes.io/part-of=kubernetes-dashboard
                  app.kubernetes.io/version=1.14.0
                  helm.sh/chart=kubernetes-dashboard-7.14.0
                  pod-template-hash=64bbbb48b
Annotations:      checksum/config: 9c2859a158b949617ca2ba9032997e8ad72fead0ad50435eca5fc37f5954c95d
                  k8s.ovn.org/pod-networks:
                    {"default":{"ip_addresses":["10.38.1.7/24"],"mac_address":"0a:58:0a:26:01:07","gateway_ips":["10.38.1.1"],"routes":[{"dest":"10.38.0.0/16"...
Status:           Running
SeccompProfile:   RuntimeDefault
IP:               10.38.1.7
IPs:
  IP:           10.38.1.7
Controlled By:  ReplicaSet/kubernetes-dashboard-api-64bbbb48b
Containers:
  kubernetes-dashboard-api:
    Container ID:  cri-o://44f88078fd5a2779ad7557dfe1ec6729f16929c5ff430e4e3b0f901bfb17a460
    Image:         docker.io/kubernetesui/dashboard-api:1.14.0
    Image ID:      docker.io/kubernetesui/dashboard-api@sha256:2bd14c0ffee99d15fb1595644ebd1083ac32c5157c6e6fd8615b0f556a1390c2
    Port:          8000/TCP
    Host Port:     0/TCP
    Args:
      --namespace=dashboard
      --metrics-scraper-service-name=kubernetes-dashboard-metrics-scraper
    State:          Running
      Started:      Tue, 27 Jan 2026 13:34:47 +0100
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     250m
      memory:  400Mi
    Requests:
      cpu:     100m
      memory:  200Mi
    Environment:
      CSRF_KEY:    <set to the key 'private.key' in secret 'kubernetes-dashboard-csrf'>  Optional: false
      GOMAXPROCS:  1 (limits.cpu)
      GOMEMLIMIT:  419430400 (limits.memory)
    Mounts:
      /tmp from tmp-volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-qhjcn (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  tmp-volume:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  kube-api-access-qhjcn:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  47m   default-scheduler  Successfully assigned dashboard/kubernetes-dashboard-api-64bbbb48b-b8vjj to wks-5325ab-00001.class.syscallx86.com
  Normal  Pulling    47m   kubelet            Pulling image "docker.io/kubernetesui/dashboard-api:1.14.0"
  Normal  Pulled     47m   kubelet            Successfully pulled image "docker.io/kubernetesui/dashboard-api:1.14.0" in 10.839s (10.839s including waiting). Image size: 55164394 bytes.
  Normal  Created    47m   kubelet            Created container: kubernetes-dashboard-api
  Normal  Started    47m   kubelet            Started container kubernetes-dashboard-api
```

#### Node management

- vypiš všechny nody
```bash
# kubectl get nodes
NAME                                    STATUS   ROLES           AGE     VERSION
ctl-5325ab-00001.class.syscallx86.com   Ready    control-plane   2d21h   v1.30.14
wks-5325ab-00001.class.syscallx86.com   Ready    worker          2d21h   v1.30.14
wks-5325ab-00002.class.syscallx86.com   Ready    worker          2d21h   v1.30.14
```

- vypiš všechny nody i s detaily
```bash
# kubectl get nodes -o wide
NAME                                    STATUS   ROLES           AGE     VERSION    INTERNAL-IP   EXTERNAL-IP   OS-IMAGE                      KERNEL-VERSION                 CONTAINER-RUNTIME
ctl-5325ab-00001.class.syscallx86.com   Ready    control-plane   2d21h   v1.30.14   10.4.1.11     <none>        Rocky Linux 9.7 (Blue Onyx)   5.14.0-611.24.1.el9_7.x86_64   cri-o://1.30.10
wks-5325ab-00001.class.syscallx86.com   Ready    worker          2d21h   v1.30.14   10.4.1.81     <none>        Rocky Linux 9.7 (Blue Onyx)   5.14.0-611.24.1.el9_7.x86_64   cri-o://1.30.10
wks-5325ab-00002.class.syscallx86.com   Ready    worker          2d21h   v1.30.14   10.4.1.82     <none>        Rocky Linux 9.7 (Blue Onyx)   5.14.0-611.24.1.el9_7.x86_64   cri-o://1.30.10

```

- zobraz všechny detaily ke konkrétnímu nodu:
```bash
$ kubectl describe node wks-5325ab-00001.class.syscallx86.com
Name:               wks-5325ab-00001.class.syscallx86.com
Roles:              worker
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=wks-5325ab-00001.class.syscallx86.com
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/worker=worker
Annotations:        k8s.ovn.org/host-cidrs: ["1.4.1.130/32","10.4.1.129/32","10.4.1.130/32","10.4.1.81/24"]
                    k8s.ovn.org/l3-gateway-config:
                      {"default":{"mode":"local","bridge-id":"br-ex","interface-id":"br-ex_wks-5325ab-00001.class.syscallx86.com","mac-address":"2e:ee:32:7b:3f:...
                    k8s.ovn.org/node-chassis-id: 4348f389-56cf-45a4-8527-e2091c93370e
                    k8s.ovn.org/node-encap-ips: ["10.4.1.81"]
                    k8s.ovn.org/node-gateway-router-lrp-ifaddrs: {"default":{"ipv4":"100.64.0.3/16"}}
                    k8s.ovn.org/node-id: 3
                    k8s.ovn.org/node-masquerade-subnet: {"ipv4":"169.254.169.0/29","ipv6":"fd69::/125"}
                    k8s.ovn.org/node-primary-ifaddr: {"ipv4":"10.4.1.81/24"}
                    k8s.ovn.org/node-subnets: {"default":["10.38.1.0/24"]}
                    k8s.ovn.org/zone-name: global
                    kubeadm.alpha.kubernetes.io/cri-socket: unix:///var/run/crio/crio.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sat, 24 Jan 2026 16:45:11 +0100
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  wks-5325ab-00001.class.syscallx86.com
  AcquireTime:     <unset>
  RenewTime:       Tue, 27 Jan 2026 14:19:40 +0100
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Tue, 27 Jan 2026 14:15:43 +0100   Sat, 24 Jan 2026 16:45:01 +0100   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Tue, 27 Jan 2026 14:15:43 +0100   Sat, 24 Jan 2026 16:45:01 +0100   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Tue, 27 Jan 2026 14:15:43 +0100   Sat, 24 Jan 2026 16:45:01 +0100   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Tue, 27 Jan 2026 14:15:43 +0100   Sat, 24 Jan 2026 16:46:23 +0100   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  10.4.1.81
  Hostname:    wks-5325ab-00001.class.syscallx86.com
Capacity:
  cpu:                2
  ephemeral-storage:  10246492Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             3743052Ki
  pods:               110
Allocatable:
  cpu:                2
  ephemeral-storage:  9443167012
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             3640652Ki
  pods:               110
System Info:
  Machine ID:                 2309824a452058d2657babac4bfa10a1
  System UUID:                b58822d1-0831-49a4-b583-d2fac0d54c92
  Boot ID:                    98b530d2-b927-4c80-a18b-4fa674d9c70d
  Kernel Version:             5.14.0-611.24.1.el9_7.x86_64
  OS Image:                   Rocky Linux 9.7 (Blue Onyx)
  Operating System:           linux
  Architecture:               amd64
  Container Runtime Version:  cri-o://1.30.10
  Kubelet Version:            v1.30.14
  Kube-Proxy Version:         v1.30.14
PodCIDR:                      10.38.1.0/24
PodCIDRs:                     10.38.1.0/24
Non-terminated Pods:          (5 in total)
  Namespace                   Name                                          CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
  ---------                   ----                                          ------------  ----------  ---------------  -------------  ---
  dashboard                   kubernetes-dashboard-api-64bbbb48b-b8vjj      100m (5%)     250m (12%)  200Mi (5%)       400Mi (11%)    45m
  dashboard                   kubernetes-dashboard-auth-579765ddf4-j46bj    100m (5%)     250m (12%)  200Mi (5%)       400Mi (11%)    45m
  dashboard                   kubernetes-dashboard-kong-76c74d5846-gvqlh    0 (0%)        0 (0%)      0 (0%)           0 (0%)         45m
  kube-system                 kube-proxy-h9mxf                              0 (0%)        0 (0%)      0 (0%)           0 (0%)         2d21h
  ovn-kubernetes              ovnkube-node-49stn                            300m (15%)    0 (0%)      900Mi (25%)      0 (0%)         2d21h
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests      Limits
  --------           --------      ------
  cpu                500m (25%)    500m (25%)
  memory             1300Mi (36%)  800Mi (22%)
  ephemeral-storage  0 (0%)        0 (0%)
  hugepages-1Gi      0 (0%)        0 (0%)
  hugepages-2Mi      0 (0%)        0 (0%)
Events:              <none>
```

#### Service management

- vypiš služby v daném ns

```bash
$ kubectl get svc -n dashboard
NAME                                   TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
kubernetes-dashboard-api               ClusterIP   10.49.158.78   <none>        8000/TCP   49m
kubernetes-dashboard-auth              ClusterIP   10.49.160.42   <none>        8000/TCP   49m
kubernetes-dashboard-kong-proxy        ClusterIP   10.49.26.202   10.4.1.129    443/TCP    49m
kubernetes-dashboard-metrics-scraper   ClusterIP   10.49.7.245    <none>        8000/TCP   49m
kubernetes-dashboard-web               ClusterIP   10.49.26.98    <none>        8000/TCP   49m
```

- vypiš ip adressy podů na které služba dělá loadbalancing (srovnej s `kubect get pods -i wide` )
```bash
$ kubectl get ep kubernetes-dashboard-kong-proxy
NAME                              ENDPOINTS        AGE
kubernetes-dashboard-kong-proxy   10.38.1.8:8443   51m
[veldrane@jump ~]$ kubectl get pods -o wide | grep 10.38.1.8
kubernetes-dashboard-kong-76c74d5846-gvqlh            1/1     Running   0          51m   10.38.1.8   wks-5325ab-00001.class.syscallx86.com   <none>           <none>
```