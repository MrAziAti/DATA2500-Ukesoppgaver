# Uke9


### **9.1 (Oblig) På forelesning ble output fra et par kommandoer brukt til å vise at kjernene på desktop'en rex var hyperthreading og til å vise hvilke to CPU'er mellom 0 og 7 (OS sin nummerering) som var thread-siblings, dvs deler ALU. Gjør det samme på Linux-VM. Er det thread-siblings på Linux-VM?***

    grep " " /sys/devices/system/cpu/cpu*/topology/thread_siblings_list
    

### **9.2 (Oblig) Kompiler det RAM-intensive programmet mem.c demonstrert på forelesning

    #include <stdio.h> 

    int array[102400];

    void main(){
    int i,k;
    for(k=0;k<2000000;k++)
        {
        for(i = 0;i < 1024;i++){
        array[i] = i;
        }
        }
    }

### **til Linux-VM, kompiler det med gcc og kjør det og ta samtidig tiden på det med time. Definer først i shellet variabelen**

    TIMEFORMAT="Real:%R User:%U System:%S %P%%"

### **for å få en ryddigere utskrift av tidsbruken. Legg gjerne denne linjen inn i .bashrc, slik at du ikke trenger å definere den på nytt hver gang du bruker time. Bruk taskset til å sørge for at to kjøringer av mem.c begge kjører på CPU nr 0. Hvor lang tid tar det før begge disse er fullført sammenlignet med om du kjører dem slik at OS bestemmer hvilken CPU de bruker? Hvordan kan det forklares?**

    
    En kjøring:
    Real:6,023 User:6,001 System:0,004 99,69%

    To kjøringer på samme cpu:
    Real:11,871 User:5,932 System:0,004 50,00%
    Real:11,903 User:5,961 System:0,004 50,11%  

    To kjøringer når OS velger CPU:
    Real:6,038 User:6,033 System:0,000 99,91%
    Real:6,041 User:6,034 System:0,005 99,96%

    Når OS velger hvilken cpu som blir brukt får disse prossessene hver sin CPU til å jobbe på. Det vil ta nesten dobbelt så lang tid hvis man setter begge prossessene på samme cpu fordi de vil dele kapasiteten til å utføre jobben. 


### **9.3 (Oblig) Ta utgangspunkt i scriptet regn som ble brukt i forelesningen til å finne ut om CPUene på desktopen rex bruker hyperthreading.

    #! /bin/bash

    (( max = 3000000 ))
    (( i = 0  ))
    (( sum = 0  ))

    while (($i < $max))
    do
            (( i += 1 ))
        (( sum += i  ))
    done
    #echo $0, resultat: $sum
  
### **Sørg først for at du kan kjøre dette og ta tiden på det som i de forrige oppgavene. På forelesningen ble kjøring og tidtaging av flere instanser av dette programmet til å avgjøre om Linux-VM har hyperthreading cores, på desktopen rex, der konklusjonen ble at det var fire hyperthreading kjerner (cores), som OS betraktet som totalt 8 CPUer. Men denne metoden er det vanskelig å bruke på Linux-VM fordi man der kun får tilgang til 2 CPUer av serverens 48 cores. Din VM er egentlig en docker-container som er startet med docker container run --cpus="2" slik at den bare får det som tilsvarer 2 CPU-er med CPU-tid. I oppgave 1 denne uken, fant du ut hvilke CPUer som er siblings. Prøv å finne ut av effekten av hyperthreading for CPUene på Linux-VM ved å samtidig kjøre regn-scriptet ved hjelp av taskset på to CPU-siblings og på to CPUer som ikke er siblings og ta tiden på dem. Utgjør dette noen forskjell utifra tiden det tar? Hva kan du konkludere utifra dette?**

    Kjøring på 2 siblings:
    for i in 0 48; do time taskset -c $i ./regn.sh& done

    Real:21.433 User:21.394 System:0.004 99.84%
    Real:21.435 User:21.378 System:0.004 99.75%

    Kjøring på 2 som ikke er siblings: 
    for i in 1 2; do time taskset -c $i ./regn.sh& done

    Real:13.307 User:13.217 System:0.000 99.32%
    Real:13.355 User:13.263 System:0.000 99.31%


    En ALU pr cpu - og siblings deler ALU`en, når prosessene kjøres på siblings vil de dele ALU og dermed bruke lenger tid.
    Når De kjøres på 2 forskjellige CPU har de hver sin ALU og får også brukt hele cpu`en til å gjøre seg ferdig med jobben.


### **9.4 Gjør tilsvarende forsøk med mem.c og følgende CPU-intensive C-program etter å ha kompilert dem med gcc -O:**
    #include <stdio.h>

    int main()
    {
    float sum = 10;
    int i,j;
    for (j = 1; j < 5;j++)
    for (i = 1; i < 450000000;i++)
        {
        sum = sum/(1.0*i);
        }
    printf("SUm: %2.6f",sum);
    }
### **Ser du noen forskjeller i effekten av hyperthreading?**

    kjøring på 2 siblings:
    for i in 0 48; do time taskset -c $i ./a.out& done
    real	0m10.483s
    user	0m10.474s
    sys	0m0.000s

    SUm: 0.000000

    real	0m10.487s
    user	0m10.473s
    sys	0m0.000s
---
    Kjøring på 2 som ikke er siblings: 
    for i in 1 2; do time taskset -c $i ./a.out& done
    real	0m10.435s
    user	0m10.421s
    sys	0m0.000s

    SUm: 0.000000

    real	0m10.438s
    user	0m10.419s
    sys	0m0.004s

    Ser ingen forkskjell på tid på disse to kjøringene. Begge bruker like lang tid. 

### **9.5 (Oblig)Følgende er en video med gjennomgang av litt av det man skal få til i de følgende Docker-oppgavene. Se den hvis du ikke får til oppgavene under.**

### **På Linux-VMene er docker installert, men man må starte docker-tjenesten. Det må man være root for å gjøre og det kan gjøres med**

    root@os100:~# service docker start
    * Starting Docker:   docker                                                   
    root@os100:~# 

### **Test deretter at docker virker ved å som root kjøre kommandoen**

    root@os100:~# docker container run hello-world
  
### **som blant annet gir output Hello from Docker! Alle docker-oppgaver må gjøres som root. Når dette fungerer, kan du begynne på oppgavene som ligger på web-siden**

    https://github.com/praqma-training/docker-exercises/tree/master/labs
### **Målet denne uken er å komme igjennom assignment 1-5. En fin måte å komme igjennom alle assignmentene er å gå igjennom Mike Longs slides fra 2018 og hver gang det kommer en slide med "Your turn", klikke deg inn på neste assignment og gjøre den (men du må legge til en 0 foran nummeret på oppgaven, 01 istedet for 1). Slidene ligger under filer i Canvas og heter Docker Kickstart.**

### **I oppgave 4-port-forward.md, skal du få opp nginx-websiden på**

    http://os100.vlab.cs.hioa.no:8080
  
### **hvor du må bytte ut os100 med din Linux-VM. Men trafikk på portnummer 8080 blir stoppet av OsloMets brannmur når forespørselen kommer utenfra. Bruk derfor 7979 som portnummer istedet for 8080.**
<br>
<br>

# **Under er oppgaver fra slides**

## **01.Hello World fungerer**
    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
        (amd64)
    3. The Docker daemon created a new container from that image which runs the
        executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it
        to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/

    For more examples and ideas, visit:
    https://docs.docker.com/get-started/

<br>
<br>

## **02.Running your first container from image**

    root@os20:/home/s354542/uke9# docker image pull alpine

    Using default tag: latest
    latest: Pulling from library/alpine
    Digest: sha256:21a3deaa0d32a8057914f36584b5288d2e5ecc984380bc0118285c70fa8c9300
    Status: Image is up to date for alpine:latest
    docker.io/library/alpine:latest

### **Docker image ls**
    docker image ls
    REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
    nginx         latest    c919045c4c2b   41 hours ago    141MB
    ubuntu        latest    54c9d81cbb44   4 weeks ago     72.8MB
    alpine        latest    c059bfaa849c   3 months ago    5.58MB
    hello-world   latest    feb5d9fea6a5   5 months ago    13.3kB
    ubuntu        14.04     13b66b487594   11 months ago   196MB

### **2.1 docker container run**

    root@os20:/home/s354542/uke9# docker container run alpine ls -l
    total 56
    drwxr-xr-x    2 root     root          4096 Nov 24 09:20 bin
    drwxr-xr-x    5 root     root           340 Mar  3 07:23 dev
    drwxr-xr-x    1 root     root          4096 Mar  3 07:23 etc
    drwxr-xr-x    2 root     root          4096 Nov 24 09:20 home
    drwxr-xr-x    7 root     root          4096 Nov 24 09:20 lib
    drwxr-xr-x    5 root     root          4096 Nov 24 09:20 media
    drwxr-xr-x    2 root     root          4096 Nov 24 09:20 mnt
    drwxr-xr-x    2 root     root          4096 Nov 24 09:20 opt
    dr-xr-xr-x 3150 root     root             0 Mar  3 07:23 proc
    drwx------    2 root     root          4096 Nov 24 09:20 root
    drwxr-xr-x    2 root     root          4096 Nov 24 09:20 run
    drwxr-xr-x    2 root     root          4096 Nov 24 09:20 sbin
    drwxr-xr-x    2 root     root          4096 Nov 24 09:20 srv
    dr-xr-xr-x   13 nobody   nobody           0 Mar  3 07:23 sys
    drwxrwxrwt    2 root     root          4096 Nov 24 09:20 tmp
    drwxr-xr-x    7 root     root          4096 Nov 24 09:20 usr
    drwxr-xr-x   12 root     root          4096 Nov 24 09:20 var

<br>

    root@os20:/home/s354542/uke9#$ docker container run alpine echo "hello from alpine"

    Hello from alpine

<br>

### **Diverse docker commands**

    root@os20:/home/s354542/uke9# docker container run alpine /bin/sh
    root@os20:/home/s354542/uke9# docker container run -it alpine /bin/sh
    / # ls
    bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    tmp    usr    var
    / # uname -a
    Linux 8a2300981b25 5.4.0-100-generic #113-Ubuntu SMP Thu Feb 3 18:43:29 UTC 2022 x86_64 Linux
    / # exit
    root@os20:/home/s354542/uke9# 

### **Starte Docker container med navn spesifisert av bruker**

    docker container run -it --name yoyo alpine /bin/sh

<br>
<br>

## **03.Throw your container away**

    root@os20:/home/s354542/uke9# docker container run -it alpine
    
    / # ls
    bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    tmp    usr    var

### **Now, delete the whole file system with rm -rf /**

    Etter sletting fungerer ingen kommandoer. Virker som at hele systemet ble slettet. 

    # ls
    /bin/sh: ls: not found
    # whoami
    /bin/sh: whoami: not found
    # date
    /bin/sh: date: not found
### **AutoSletting av container etter bruk**
    docker container run --rm -it alpine

### **Sletting av containere**
    docker container rm <navn> / <id>

### **Sletting av image**
    docker image rm <navn> / <id>

### **Cleaning up**

    docker container prune
    docker image prune
    docker network prune
    docker volume prune

## **04.A basic webserver - Port forwarding**

    Starte en webserver med Nginx

    docker container run -p 8080:80 nginx

### **Kjøre webserver i bakgrunnen**

    docker container run -d -p 7979:80 nginx

<br>

## **05.Executing processes in your container**

    docker container exec -it CONTAINERNAME bash

    kommando over starter bash for containeren

    Lokalisert index.html filen og endret den og sett at endring skjer på websereveren. 



## **(oblig)9.6(Oblig) Start et ubuntu-container og inkluder -p 8081:80, slik at man kan koble til en webserver på port 8081 på Linux-VM. Gå inn i containeren på kommandolinjen og installer apache2 webserver og få den til å kjøre. Prøv også å få webserveren til å starte og å endre innholdet på webserveren fra kommandolinjen på Linux-VM. Sjekk at du kan se webserveren på**

    http://os100.vlab.cs.hioa.no:8081/

    Starter ubuntu:

    docker container run -it -p 8081:80  ubuntu /bin/bash

    Innstallerte apache2 og sjekket at det fungerte

    gjorde endringer i html med echo docker20 > index.html og sjekket at det fungerte
  
  <p align="center">
<img src="/Users/aziz/Documents/GitHub/DATA2500-Ukesoppgaver/Bilder/Skjermbilde 2022-03-03 kl. 10.26.33.png">

### **hvor du må bytte ut os100 med din Linux-VM. Når du har fått installert apache2 og fått den til å kjøre, gå ut av containeren med CTRL-p CTRL-q (da fortsetter den å kjøre i bakgrunnen) og list kjørende containere med**

    # docker container ps -a

    docker ps -a
    CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS                         PORTS                  NAMES
    657a210753d5   ubuntu         "/bin/bash"              7 minutes ago       Up 7 minutes                   0.0.0.0:8081->80/tcp   determined_euclid
    cc77f04b67c4   ubuntu         "/bin/bash"              12 minutes ago      Exited (0) 8 minutes ago                              eager_maxwell
    58a306185482   ubuntu         "/bin/bash"              14 minutes ago      Exited (0) 13 minutes ago                             sleepy_hypatia
    ac070f7f024c   nginx          "/docker-entrypoint.…"   20 minutes ago      Exited (0) 19 minutes ago                             priceless_allen
    314adf2c716a   nginx          "/docker-entrypoint.…"   21 minutes ago      Exited (0) 21 minutes ago                             reverent_curie
    222c295d6f1d   nginx          "/docker-entrypoint.…"   58 minutes ago      Exited (0) 54 minutes ago                             some-nginx
    0a6e116149ef   nginx          "/docker-entrypoint.…"   About an hour ago   Up About an hour               0.0.0.0:7979->80/tcp   vigorous_shamir
    ceed426bd02f   nginx          "/docker-entrypoint.…"   About an hour ago   Exited (0) About an hour ago                          wonderful_pascal
    8754b66d012b   nginx          "/docker-entrypoint.…"   About an hour ago   Exited (0) About an hour ago                          serene_mestorf
    12b1b97465b4   alpine         "/bin/sh"                2 hours ago         Exited (127) 2 hours ago                              boring_varahamihira
    8b90fc98611e   alpine         "/bin/sh"                2 hours ago         Exited (0) 2 hours ago                                yoyo
    08f89b6fbc4f   alpine         "/bin/sh"                2 hours ago         Exited (0) 2 hours ago                                agitated_mcclintock
    8a2300981b25   alpine         "/bin/sh"                2 hours ago         Exited (0) 2 hours ago                                vibrant_tu
    27505a374892   alpine         "/bin/sh"                2 hours ago         Exited (0) 2 hours ago                                jolly_gagarin
    089a37259f62   alpine         "/bin/bash"              2 hours ago         Created                                               awesome_lamport
    562a96887dd4   alpine         "echo 'Hello from al…"   2 hours ago         Exited (0) 2 hours ago                                funny_kirch
    5ef51ad79974   alpine         "ls -l"                  2 hours ago         Exited (0) 2 hours ago                                jolly_keldysh
    335c07ea8769   ubuntu:14.04   "/bin/bash"              2 hours ago         Exited (0) 2 hours ago                                sad_brown
    b43397325882   alpine         "echo 'Hello from al…"   2 hours ago         Exited (0) 2 hours ago                                stupefied_perlman
    fd1838d70043   alpine         "ls -l"                  2 hours ago         Exited (0) 2 hours ago                                nice_ishizaka
    6228df598154   alpine         "ls-l"                   2 hours ago         Created                                               interesting_chaum
    b9a990ce2ac4   ubuntu         "/bin/bash"              15 hours ago        Exited (0) 15 hours ago                               agitated_pascal
    17060528d8aa   nginx          "/docker-entrypoint.…"   15 hours ago        Exited (0) 15 hours ago                               silly_snyder
    4936851d5240   nginx          "/docker-entrypoint.…"   15 hours ago        Exited (0) 15 hours ago                               vibrant_shannon
    e6937596f3a3   nginx          "/docker-entrypoint.…"   15 hours ago        Exited (0) 15 hours ago                               brave_poitras
    bdcc87e0d001   hello-world    "/hello"                 15 hours ago        Exited (0) 15 hours ago                               angry_gates

  
### **Da vil du for containeren du har installert apache i, få opp en linje som ser ut omtrent slik:**

    3376df05f434        ubuntu        "/bin/bash"         3 minutes ago       Up 3 minutes                  0.0.0.0:8081->80/tcp   elegant_almeida

### **Lag så en kopi av denne containeren med**
 
    docker container commit 3376df05f434 apacheubuntu
### **eventuelt ved å bruke docker export og import. Etter å ha gjort dette, kan du starte opp en ny container med apache installert ved

    # docker container run -it -d -p 8082:80 apacheubuntu /bin/bash
### **Deretter kan du starte apache i denne containeren ved å gjøre**

    docker container exec IDTILNYCONTAINER /bin/bash -c "/etc/init.d/apache2 start"


### **hvor IDTILNYCONTAINER er id til den nye containeren du nettopp startet (returneres av kommandoen du startet med, kan også sees med # docker container ps -a). Endre så /var/www/html/index.html på begge docker-instansene slik at du kan se hvem som er hvem når du åpner webserverene i en browser.**