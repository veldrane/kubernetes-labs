## Obecné informace

image-name: simple-api  
install version: v1.1.0 (pozor stara verze neumi config file) 
location: registry.class.syscallx86.com

- template manifestu pro deployment: `manifests/de-simple-api.yaml`
- template minifestu pro configmapu: `manifests/cm-simple-api.yaml`
- configurace aplikace: `appconfig/config.yaml`

### Aplikace simple api

```
$ ./simple-api-rs --help
A simple api for testing purposes with various infrastructure features

Usage: simple-api-rs [OPTIONS]

Options:
  -c, --config <CONFIG>  config file path
  -h, --help             Print help
  -V, --version          Print version
```


## Cíl


## Úlohy

- vytvoř namespace `simple-api` a přepni se do něj
    - kubectl create command
- naclonuj si repozitář `github.com/veldrane/kubernetes-app`
    - git clone
- přečti si soubor README a najdi deployment manifest  
- vytvoř aplikační configmapu simple-api-config ve která bude obsah souboru config.yaml
- uprav manifest tak aby:
   - v rámci deploymentu jsi připojil configmapu jako volume simple-api-config
   - tento volume jsi namountoval do adresáře /etc/simple/config.yaml
   - vytvoř v deploymentu args tak, aby aplikace použila config.yaml jako konfigurační soubor
   - přes `kubectl create -f <manifest>` ho vytvoř v namespace simple-api
- Nastartoval pod v pořádku ?
- Pokud ne tak proč ne :)
    - případná diskuse plus troubleshooting
- uprav parametry aplikace min-delay, max-delay a error-rate na vyšší hodnoty
- z debug contejneru zkoušej curl na pod aplikace a příslušný port a sleduj její chování
- smaž deployment  z clusteru
- rozšiř deployment manifest o sekci containerPorts

```
    ports:
    - name: http
      containerPort: 8080
      protocol: TCP
```

- aplikuj deployment znovu a přes příkaz `kubectl expose deployment <nazev deploymenut> vytvoř objekt service
    - jakou ma ip adresu ?
    - zkus curl přístup na aplikační pody přes curl http://<svc ip>/api/v1/articles -v
        - z debug nodu
        - z jump serveru 
    - dále by měl fungovat resolving který nativně kubernetes poskytuje:
        `curl http://<svc-name>.<ns name>.svc.cluster.local

- přes kubectl patch nastav service external ip na 10.4.<subnet>.130

```bash
kubectl patch svc simple-api -p '{"spec":{"externalIPs":["10.4.1.130"]}}'
```
- zkus znovu curl z jump serveru
- změn přes webui frontend port z portu 8080 na 80 a znovu zkus curl
- jak cluster ppozna jaká služba odkazuje na jaké pody ?