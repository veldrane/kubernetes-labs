### Obecné informace

image-name: simple-api  
install version: v1.0.0  
location: registry.class.syscallx86.com

Cíl:

Vydeplojovat aplikaci do ns

### Deploy aplikace do clusteru

- vytvoř namespace `simple-api` a přepni se do něj
    - kubectl create command
- naclonuj si repozitář `github.com/veldrane/kubernetes-app`
    - git clone
- přečti si soubor README a najdi deployment manifest  
- zadej správnou cestu k image v depoyment na registry `registry.class.syscallx86.com`
    - image samotna je simple-api:v1.0.0
- uprav manifest, nastav správnou cestu k image a aplikuj ho na svůj cluster
    - manifesty jsou tu dva, dle Kind Kind zjistíš který je deployment
    - příkaz kubectl create 
- sleduj startování podu `simple-api`
    - prikaz kubectl get
- pokud pod nenaběhne (nebude ve stavu running)
    - podívej se na eventy `kubectl get events`
    - na status podu
    - na jeho description
- podívej se na logy podu `simple-api-pod`
    - kubectl log -f 
- zjisti ip adresu podu a na kterém nodu běží
- otevři si druhý terminál a přihlas se pod svým účtem na jump
- zpřes curl zkus get na ip adresu simple-api podu a endpoint /api/v1/articlies
- přihlas se do debug kontejneru
    - interni prikaz `dbgpod`
    - kontejner je v debug-ns a můžeš se na něj podívat přes kubectl get pods nebo webui
    - přes curl zkus get na ip adresu simple-api podu a endpoint /api/v1/articlies
    - v logu simple-api podu by si mel vidět své requesty
- přes zvětši počet replik na 2
    - příkaz `kubectl scale`
- sleduj status podu
- smaž deployment z kubernetes
    - příkaz `kubectl delete`