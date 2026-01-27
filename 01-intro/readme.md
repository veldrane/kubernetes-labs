#### Kubernetes: Úvod

- přihlas se na jump server pomocí ssh  
- vyzkoušej základní operace pomocí příkazů `kubectl`. Použij tahák (cheatsheet) nebo jakýkoliv zdroj na internetu podle vlastní preference  
  - vypiš všechny namespaces v clusteru
  - vypiš všechny nody v clusteru  
    - co je control-plane a co jsou worker nodes ?
    - vyber si jeden node a podívej se na jeho detaily  
    - jakou má IP adresu?
    - kolik má paměti a kolik cpu
  - přihlas se na jeden z workernodu a přepni pře su na roota
    - vypiš si informace o procesorech
    - vypiš si informace o paměti
    - porovnej s výpisem přes příkaz kubectl
  - přepni se do namespace `dashboard`
  - vypiš všechny pody v tomto namespace  
  - podívej se na detaily konkrétního podu  
    - jak se jmenuje?  
    - jakou má IP adresu?  
    - na kterém nodu běží?

- přihlas se na console0x.syscall86.com
    - použij přikaz `token` k vygenerování přihlašovacího tokenu


Advanced: (pro ty co byli na předchozím školení :)
    - vyber si jeden worker node
    - přishlas se na něj a přepni na roota
    - použij příkaz `crictl ps`
    - porovnej to s výpisem podů třeba namespacu dashboard
    - co vidíš ? Mohl bys ses zkusit přepnout do kontextu podu ?