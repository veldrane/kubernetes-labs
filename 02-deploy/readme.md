### Obecné informace

image-name: simple-api  
install version: v1.0.0  
location: registry.class.syscallx86.com  

### Deploy aplikace do clusteru

- vytvoř namespace `simple-api`  
- přepni se do tohoto namespace  
- stáhni repozitář `github.com/veldrane/kubernetes-app`  
- přečti si soubor README a najdi deployment manifest  
- najdi správnou cestu k imagi v `registry.class.syscallx86.com`  
- uprav manifest, nastav správnou cestu k imagi a aplikuj ho na svůj cluster  
- sleduj startování podu `simple-api`  
- podívej se na logy podu `simple-api-pod`