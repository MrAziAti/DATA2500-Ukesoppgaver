# Uke 2

## **2.1. Hva er det to viktikste oppgavene til et operativ system**
    1. Gi applikasjonsprogrammer og brukere enhetlig, enklere og mer abstrakt adgang til maskinens ressurser
    2. Administrere ressursene slik at prosesser og brukere ikke ødelegger for hverandre når de skal aksessere samme ressurser.
---
<br>
<br>

## **2.2 I figuren i forelesningsnotatene er det to feil i output på høyre side, hva er galt?**
    1. Or skal være 0 siden input er 1 og 0. Siden en av inputene er 0 så skal output være 0.
    2. Not skal være 1 siden input er 0
---
<br>
<br>

## **2.3 Fra en Windows_PC, last ned programmet Digital.exe og and.dwm (NB! Ikke bruk Edge eller IE fra Windows, da lagres ikke dwm-filer som and.dwm riktig). Klikk på Digital for å starte simulatoren og åpne filen and.dwm.** 
---
### **Klikk på Step-knappen øverst i venstre hjøren og få resultatet for NOT-porten til å bli rødt. Rødt=1, Hvitt = 0. Velg pekefingeren fra samme meny, endre på verdiene for input og klikk igjen på step-knappen slik at det endrer seg.**

    NOT port før endring
<p align="center">
<img src="/Users/aziz/Documents/GitHub/DATA2500-Ukesoppgaver/Bilder/NotPort.png">
</p>

    NOT port etter endring
<p align="center">
<img src="/Users/aziz/Documents/GitHub/DATA2500-Ukesoppgaver/Bilder/NotPortEtterEndring.png">
</p>

---

### **Forklar utifra sannhetsverditabellene til AND og OR-portene hvorfor resultatet i den nederste kretsen blir 0, når øverste input er 1(rødt) og nederste input er 0(hvitt).**
    Nederste input går inn i en OR port og i en OR port trenger bare en av input`ene til å være 1. Øverste input går i en AND gate og der trenger begge input`ene å være 1 for å få 1 ut. 

---
### **Sett opp sannhetsverditabellen for den nederste kretsen, både utifra teoretiske beregninger med utgangspunkt i virkemåten til AND og OR og ved å teste ut alle muligheter når du kjører den nederste kretsen and.dwm i simulatoren Digital.exe.**

    | A | B | A AND B | AND OR B |
    |---|---|---------|----------|
    | 1 | 1 | 1       | 1        |
    | 0 | 1 | 0       | 1        |
    | 1 | 0 | 0       | 0        |
    | 0 | 0 | 0       | 0        |

---
<br>
<br>

## **2.4 Innledende oppgaver for deg som har lite erfaring med Linux kommandolinje**

### **For å utføre en kommando, skriver du den inn ved promptet og trykker RETURN. Når du logger inn på denne måten, vil du alltid komme til din hjemmekatalog/mappe. Det er bare her du har lov til å lage nye filer og mapper(også kalt kataloger eller på engelsk directories). Skriv inn kommandoen**

    $ pwd = /home/s354542

### **og trykk RETURN (du skriver bare inn pwd, dollar-tegnet står der fra før). Når du gjør dette, spør du operativsystemet Linux om i hvilken mappe du befinner deg (pwd = Print Working Directory). Slik snakker du altså med operativsystemet og kan både hente ut informasjon og be om å få utført ting du vil ha gjort. Språket Linux forstår, består av litt kryptiske forkortelser, men du trenger ikke å kunne så veldig mange før du snakker flytende Linux og klarer det meste.**

### **Gir du kommandoen pwd rett etter du har klikket på terminalikonet, finner du ut hva hjemmekatalogen din heter og hvor i filsystemet den befinner seg. Prøv på samme måte kommandoene**

    $ whoami = s354542

### **som gir deg brukernavnet ditt**

    $ hostname = data2500

### **som gir deg navnet på maskinen du er logget inn på**

    $ mkdir nymappe
### **som lager en ny mappe og**
    $ ls -l

### **som viser alle filer og mapper i mappen du nå står i. -l er en såkalt opsjon som endrer måten kommandoen virker på. I dette tilfellet gir det mer detaljert informasjon en bare ls ville gitt. Prøv!**
---
<br>
<br>

## **2.5 Klikk på 'Linux hjelp'-linken på kurshjemmesiden og les og prøv ut det som står under 'Nyttige tips om bruk av Linux' fra kommandolinjen.**

    lest


<br>
<br>

## **2.6 Klikk på 'Linux hjelp'-linken på kurshjemmesiden og prøv å finne ut under linken 'Linux kommando oversikt' hvordan man gir en kommando som viser innholdet av en fil på skjermen. Prøv å se på innholdet av filen /etc/passwd.**

    kommando heter CAT. F eks kan man kjøre cat fil.txt som viser innholdet av fil.txt på skjermen.

## **2.7 Finnes ikke**
    finner ikke oppgaven på websiden
<br>
<br>

## **2.8 Kommandoen som lager et nytt directory(katalog/mappe) heter mkdir. Lag et directory som heter oblig1.**

    mkdir oblig1

<br>
<br>

## **2.9 Kommandoen som lager en tom fil, eller oppdaterer tidstemplet på filer som ekisterer fra før heter touch. Lag en tom fil ved å skrive touch oblig1/newfile.C.**

    touch oblig1/newfile.c

<br>
<br>

## **2.10 Bruk Linux kommando-oversikten under Linux-hjelp til å finne kommandoene som skal til for å løse denne oppgaven. Gå inn i oblig1 directoryet ved å skrive cd oblig1. Lag en kopi av filen og gi den navnet newer.C. Bruk kommandoen ls til å se at begge filen ligger der. Slett deretter filen newfile.C.**

    Cp newfile.C newer.C – lager ny fil som heter newer.C
    Slette filen – rm newfile.C

## **2.11 Lag en katalog (directory) som heter newkat og en fil i denne katalogen med navn newFile.txt som inneholder linjen "ny". Fjern etterpå begge deler.**
    Mkdir newkat
    Cd newkat
    Nano newfile.txt får å få opp teksteditor og skrive ny.
    cd ..
    Rm -r newkat

<br>
<br>

## **2.12 Det ligger mange filer i ditt hjemme-område som blir brukt av software til å lagre oppsett. Disse heter .et-eller-annet. Filer som begynner på "." skjules vanligvis. Tast inn en kommando som lister alle filene i hjemmekatalogen din, inkludert de skjulte. Hva betyr filene "." og ".." ? (hint: prøv å gå til dem med cd)**

    kommando: ls -a - som lister alle filer samt de skjulte filene.
    .. referer til filen/mappen over den du står i. Med cd .. kan du bevege deg en level opp i fil strukturen
    . referer til mappen du står i.

<br>
<br>

## **2.13 (Oblig) Bruk mkdir, cp og touch til å opprette en katalogstruktur som den på figuren, der passwd er en kopi av systemets passordfil mens fil1 og fil2 er tomme filer. Katalogen ~ er din hjemmekatalog.**

    Mkdir tmp
    Cd tmp
    Touch passwd
    Cp /etc/passwd passwd
    Mkdir etc
    Cd etc
    Mkdir bin
    Touch fil2

### Under vises katalokstrukturen med kommandoen tree
    -- tmp
    |-- etc
    |   |-- bin
    |   `-- fil2
    |-- fil1
    `-- passwd

<br>
<br>

## **2.14 (Oblig) Gi en kommando som flytter deg to kataloger oppover i filtreet.**
    cd ../..

<br>
<br>

## **2.15 (Oblig) Lag en mappe i din brukers hjemmekatalog. Gå inn i den mappen og lag noen tomme filer med kommandoen touch filnavn. Kopier alle filer i katalogen du står i som slutter på .java til katalogen over deg. Sørg for at du har laget noen slike filer først.**

    Mkdir nymappe
    Laget flere filer i nymappe
    Flytter alt fra nymappe over til hjemmekatolen -  cp nymappe/*.java . 
    Jeg stod i hjemmemappen når jeg kjørte kommando over. 

<br>
<br>

## **2.16 (Oblig) List alle filer og kataloger under /usr/bin som har filnavn som begynner på "b".**

    ls -d /usr/bin/b*

<br>
<br>

## **2.17 Bruk online manualen man i et shell vindu til å slå opp unix kommmandoene mkdir, echo og type man mkdir Lesingen av en side kan avsluttes ved å taste "q" for quit. Ikke les alle detaljer, bare de første linjene. Dette er for at du senere skal vite hvor du kan finne detaljert informasjon om Linux-kommandoer. Det finnes ingen egen manualside for type fordi det er en såkalt 'shell builtin' og en del av shellet. Men den står omtalt nesten helt til slutt i den lange manualen om bash ($ man bash). Prøv også kommandoen help type.**

    man mkdir
    man echo
    man find 
    etc

<br>
<br>

## **2.18 (Oblig) I denne oppgaven skal du lage et lite shellscript. Start en editor med**
## $ jed info.sh 
## og skriv inn 
## #! /bin/bash 
## whoami
## hostname 
## uname -a

## **og lagre filen. Dette er et lite shellscript med navn info.sh som utfører de tre kommandoene når du kjører det. For at det skal bli kjørbart, må du sette kjørerettigheter på scriptet med**

## $ chmod 700 info.sh

## **og du skal kunne kjøre det ved å taste inn kommandoen**

## $ info.sh
## **Hvis det ikke går, prøv**
## $ ./info.sh

## **Hva er forskjellen på de to måtene å kjøre scriptet på?**


    Jeg forsøkte å kjøre scriptet med info.sh og det fungerte ikke. Fikk melding om at command not found. 

    Fungerer fint med ./info.sh og . info.sh

    Dette fordi man på å definere hvor man ønsker å kjøre scriptet i fra. Den første kommandoen (info.sh) vil ikke fungere fordi man ikke definerer plassen hvor denne ligger. 

## **2.19 (Oblig) top til overvåking av prosesser og brukere. Hvis du står fast på noen av de følgende oppgavene, se gjerne på siste del av den digitale Linux-forelesningen fra uke 1:**

    linux1del9.mp4 (03:47) Demo: Hvordan dokumenter oppgaver og hint til top og psuser-oppgavene 

## **top er en kjent og kjær kommando for å få et inntrykk av hva som skjer på systemet. Den gir en mengde informasjon til brukeren om systemets tilstand og de kjørende prosessene.Start top i kommandolinjen og forklar hva du ser. Beskriv hvordan top er delt opp i to visuelle deler. Beskriv hva de to forskjellige delene viser og nevn de to datafeltene du mener er mest interessant i den øverste delen. For en forklaring av alle feltene, se "man top". Prøv å taste "1" i top. Hva skjer og hvilken ekstra info får du nå? (tast "1" på nytt for å gå tilbake til slik det var)**

    Øverste delen viser statistikk over prosesser og ressursbruk og den nedre delen inneholder en liste over prosesser som kjører for øyeblikket. 

    Med kommando 1 i TOP ser jeg at CPU biten deler seg til CPU 1 og CPU 2. Altså  man ser hvor mange CPU`er denne maskinen kjører. 

    De to mest interessante feltene i den øverste delen for min del må være minnebruken samt tasks biten. Altså se hvor mange prosesser som kjører, hvor mange har stoppet samt hvor mange som sover.


<br>
<br>

## **2.20 (Oblig) Top har flere "hotkeys" av typen "1" som man kan bruke til å forandre hva som vises. Prøv å taste "U" i top og så ditt eget brukernavn og se hva som skjer. Ser du noe gevinst med å bruke top på denne måten? Gi eksempel på situasjoner hvor dette kan være nyttig.**


    Kan være greit å kunne se hvor mange ressurser en user bruker. Hvor lenge en prosess har kjørt f eks hos en bruker. Hvor mye cpu og memory eventuelt de bruker. 


<br>
<br>

## **2.21(Oblig)I de neste oppgavene skal du lage ditt eget alternativ til hva du fikk til i forrige oppgave. Du skal lage et shell-script som lister opp alle prosessene til en bruker.Prøv kommandoen "ps aux". Forklar kort utskriften til den kommandoen.**

    Viser en utskrift av alle prosessene på maskinen.

<br>
<br>

## **2.22 (Oblig) grep er en kommando som kan plukke ut linjer som matcher en spesiell tekst. For at grep skal kunne plukke ut enkelte linjer fra ps aux, må vi lime dem sammen på et vis. Dette gjør vi med en pipe (engelsk for rør, pipe-tegnet er til venstre for 1-tasten):**

    ps aux | grep  tekst
## **Prøv ut den kommandoen selv og bytt ut "tekst" med noe mer fornuftig, f.eks et brukernavn. Forklar utskriften du får nå. Lag et shellscript som heter "psuser" som utfører denne kommandoen.**

    script:
    #! /bin/bash  

    ps aux | grep s354542

<br>
<br>

## **2.23 (Oblig) Det kan være praktisk å ikke måtte endre selve koden når man vil endre litt på hvordan et script kjører. Utvid shellscriptet "psuser", slik at det kan kjøres på denne måten: ./psuser root og det da skriver ut alle linjer som inneholder teksten root. Hint: inne i scriptet vil argumentet root legges i variabelen $1. Dermed kan du erstatte teksten du vil lete etter med $1.**

    #! /bin/bash

    ps aux | grep $1

<br>
<br>

# **Ukens utfordringer!**

## **Ukens utfordring nr. 1**
## **Finn ut hvilket program (hvor det ligger) som startes opp når du gir kommandoen ls. (hint: prøv  type ls, eventuelt $ unalias ls først). Editer en fil i din hjemmekatalog og kall den ls. Skriv inn følgende shell-script:**

    #! /bin/bash** 

    ls

## **Gjør scriptet ls kjørbart ved hjelp av kommandoen chmod**

    755 ls. 

## **Gi kommandoen**

    ls. 
    
## **Er det "din" eller systemets ls som blir utført ? Legg inn linjen**

    echo Dette er mitt ls script.
## **før ls-kommandoen i ditt ls-script og prøv å få systemet til å liste filene med ditt script**

    med kommandoen LS så brukes systemets LS som blir utført /usr/bin/ls

    men hvis jeg hvis jeg definerner hvor jeg ønsker å kjøre scriptet mitt fra så kjøres mitt script.

    kommando ./ls -> da kjøres mitt script

<br>
<br>

## **Ukens utfordring nr. 2:**

## **Lag en katalog med navn x. Gå til x, start en editor, skriv noen tegn og lagre filen under navnet -x. Prøv å skifte navn på filen med mv fra -x til x.txt. Hva skjer? Hvordan er det mulig å endre navnet ?**

    Får denne feilmeldingen når jeg prøver å endre navn fra -x til x.txt
    mv: invalid option -- 'x'
    Try 'mv --help' for more information.