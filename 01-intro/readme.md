#### Kubernetes: Úvod

### Cíl 

Seznámení se s prostředím

### Úlohy

- přihlas se na jump server pomocí ssh<br><br>
- vyzkoušej základní operace pomocí příkazů `kubectl/oc`. Použij tahák (cheatsheet) nebo jakýkoliv zdroj na internetu podle vlastní preference
  - vypiš všechny namespaces v clusteru
    - tip: příkaz *oc/kubectl* akce je *get* a objekt je *ns* nebo *project* v případě oc <br><br>
  - vypiš všechny nody v clusteru
    - tip: stejný příkaz i akce jako v předchozím případěm objekt je *node*, api umí i množné číslo <br>
    otázky:
      - co je control-plane a co jsou worker nodes ?<br><br>
  - vyber si jeden node a podívej se na jeho detaily
    - tip: akce je tentokrát *describe* a objekt *jméno nodu*<br>
    otázky:
      - jakou má IP adresu?
      - kolik má paměti a kolik cpu<br><br>
  - přihlas se na jeden z workernodu a přepni pře su na roota
    - vypiš si informace o procesorech
      - tip: příkaz *top* nebo *cat /proc/cpuninfo*
    - vypiš si informace o paměti
      - tip: příkaz *top* nebo *cat /proc/meminfo*
    otázky:
      - jaké zdroje vidíš přes kubernetes nástroje ?
      - jaké na nodu samotném ?<br><br> 
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
    - porovnej to s výpisem podů třeba namespace dashboard
    - co vidíš ? Mohl bys ses zkusit přepnout do kontextu podu ?