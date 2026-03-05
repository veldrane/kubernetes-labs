# Kubernetes: Deploy aplikace do clusteru

## Obecné informace


image-name: simple-api  
install version: v1.0.0  
location: registry.class.syscallx86.com

## Cíl

Seznámení se základními objekty kubernetes a workflow při deploymentu aplikcí a contejnerů

### Úlohy

- vytvoř namespace `simple-api` a přepni se do něj
    - tip: příkaz *kubectl create command*<br>
- naclonuj si repozitář `github.com/veldrane/kubernetes-app`<br>
- přečti si soubor README a najdi deployment manifest<br>
- uprav manifest tak abys:
    - zadal správné docker registry
    - jméno image
    - verzi
- manifest aplikuj svůj cluster a namespace
    - tip: *kubectl* příkaz, akce *create* nebo *apply*, *-f <manifest>*<br>
- sleduj startování podu *simple-api*
    - prikaz kubectl get
- pokud pod nenaběhne (nebude ve stavu running)
    - podívej se na eventy *kubectl get events*
    - na status podu
    - na jeho description
    - tip: viz přechozí úlohy<br>
- podívej se na logy podu *simple-api-pod*
    - tip *kubectl/oc log -f <jméno podu>*<br>
- zjisti ip adresu podu a na kterém nodu běží<br>
- otevři si druhý terminál a přihlas se pod svým účtem na jump<br>
- přes curl zkus get na ip adresu simple-api podu a endpoint /api/v1/articlies
  - otázky: je endpoint z jump serveru dostupný ?<br>
- přihlas se do debug kontejneru
    - tip: interní příkaz *dbgpod*, nebo *oc rsh <jméno pod> -n <jméno namespacu>* 
    - kontejner je v debug-ns a můžeš se na něj podívat přes kubectl get pods nebo webui
    - přes curl zkus get na ip adresu simple-api podu a endpoint /api/v1/articlies
    - v logu simple-api podu by si mel vidět své requesty
- přes zvětši počet replik na 2
    - tip: příkaz *kubectl scale*<br>
- sleduj status podu
- smaž deployment z kubernetes
    - tip: příkaz *kubectl delete*