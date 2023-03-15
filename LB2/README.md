<a name="m300-leistungsbeurteilung-2"></a>
# M300 Leistungsbeurteilung 2
Plattformübergreifende Dienste in ein Netzwerk integrieren

<a name="autor"></a>
## Autor
Tharsan Pethurupillai

<a name="inhaltsverzeichnis"></a>
## Inhaltsverzeichnis

- [M300 Leistungsbeurteilung 2](#m300-leistungsbeurteilung-2)
  - [Autor](#autor)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
  - [Einführung](/README.md#einführung)
    - [Git einrichten](/README.md#git-einrichten)
  - [Markdown](/README.md#markdown)
  - [Umgebung auf eigenem Notebook eingerichtet und funktionsfähig](/README.md#umgebung-auf-eigenem-notebook-eingerichtet-und-funktionsfähig)
    - [VirtualBox](/README.md#virtualbox)
    - [Visualstudio-Code](/README.md#visualstudio-code)
    - [Git-Client](/README.md#git-client)
    - [SSH-Key für Client erstellt](/README.md#ssh-key-für-client-erstellt)
  - [Eigene Lernumgebung (PLE) ist eingerichtet](/README.md#eigene-lernumgebung-ple-ist-eingerichtet)
    - [GitHUB oder Gitlab-Account ist erstellt](/README.md#github-oder-gitlab-account-ist-erstellt)
    - [Git-Client wurde verwendet](/README.md#git-client-wurde-verwendet)
  - [Vagrant](#vagrant)
    - [Befehle](#befehle)
    - [Netzwerkplan](#netzwerkplan)
    - [Eingerichtete Umgebung - Dokumentierung Code](#eingerichtete-umgebung---dokumentierung-code)
    - [Bestehende VM aus Vagrant-Cloud einrichten](#bestehende-vm-aus-vagrant-cloud-einrichten)
    - [Funktionsweise getestet inkl. Dokumentation der Testfälle](#funktionsweise-getestet-inkl-dokumentation-der-testfälle)
      - [Testfall für die Funktionalität](#testfall-für-die-funktionalität)
    - [andere, vorgefertige VM auf eigenem Notebook aufgesetzt](#andere-vorgefertige-vm-auf-eigenem-notebook-aufgesetzt)
    - [Benutzer- und Rechtevergabe ist eingerichtet](#benutzer--und-rechtevergabe-ist-eingerichtet)
    - [Zugang mit SSH-Tunnel abgesichert](#zugang-mit-ssh-tunnel-abgesichert)
    - [Sicherheitsmassnahmen](#sicherheitsmassnahmen)
    - [Vergleich Vorwissen - Wissenszuwachs](#vergleich-vorwissen---wissenszuwachs)
    - [Reflexion](#reflexion)
      - [Tag 1](#tag-1)
      - [Tag 2](#tag-2)
      - [Tag 3](#tag-3)
      - [Tag 4](#tag-4)
- [Bewertungsraster Leistungsbeurteilung 2](/LB2/M300-LB2-Bewertungsraster-Pethurupillai.xlsx)

## Vagrant
 > [⇧ **Nach oben**](#inhaltsverzeichnis)

Vagrant ist eine freie Ruby-Anwendung zum Erstellen und Verwalten virtueller Maschinen.[2] Vagrant ermöglicht einfache Softwareverteilung (englisch Deployment) insbesondere in der Software- und Webentwicklung und dient als Wrapper zwischen Virtualisierungssoftware wie VirtualBox, KVM/QEMU, VMware und Hyper-V und Software-Configuration-Management-Anwendungen beziehungsweise Systemkonfigurationswerkzeugen wie Chef, Saltstack und Puppet.

![image](https://user-images.githubusercontent.com/125886136/221587053-63c267aa-be05-4716-a107-02648a029add.png)

### Befehle
 > [⇧ **Nach oben**](#inhaltsverzeichnis)

| Befehl                    | Beschreibung                                                      |
| ------------------------- | ----------------------------------------------------------------- | 
| `vagrant init`            | Initialisiert im aktuellen Verzeichnis eine Vagrant-Umgebung und erstellt, falls nicht vorhanden, ein Vagrantfile |
| `vagrant up`              |  Erzeugt und Konfiguriert eine neue Virtuelle Maschine, basierend auf dem Vagrantfile |
| `vagrant ssh`             | Baut eine SSH-Verbindung zur gewünschten VM auf                   |
| `vagrant status`          | Zeigt den aktuellen Status der VM an                              |
| `vagrant port`            | Zeigt die Weitergeleiteten Ports der VM an                        |
| `vagrant halt`            | Stoppt die laufende Virtuelle Maschine                            |
| `vagrant destroy`         | Stoppt die Virtuelle Maschine und zerstört sie.                   |

Weitere Befehle unter: https://www.vagrantup.com/docs/cli/

<br>

### Netzwerkplan
<br>
Zu sehen ist mein Netzwerkplan.
Die Server- und Userspezifische Einstellungen werden im Vagrantfile getätigt. Darunter fallen z.B. Firewallrules.
Danach wird im Vagrantfile noch die Befehle eingetragen, welches der VM dann benötigt, um sich mit den Docker-Repository zu verbinden.
<br>

![image](https://user-images.githubusercontent.com/125886136/224710421-5e93c5f5-c108-4dc1-a145-d723d1370756.png)


### Eingerichtete Umgebung - Dokumentierung Code
 > [⇧ **Nach oben**](#inhaltsverzeichnis)

Hier sieht man den verwendeten Code und die Erklärung zu den jeweiligen Commands.

Vagrant konfiguration einleiten

    `Vagrant.configure(2) do |config|`


Welche Ubuntu Version verwendet wird
    
    `config.vm.box = "ubuntu/xenial64"`


Port forwarding von 80 auf 100.
    
    `config.vm.network "forwarded_port", guest:80, host:100, auto_correct: false`


Bestimmen mit welchem Programm die VM erstellt werden soll
    
    `config.vm.provider "virtualbox" do |vb|`


Festlegen wieviel Arbeitsspeicher verwendet werden darf
    
    `vb.memory = "1024"`

Ende der Vagrant Config
    
    `end`


VM Config einleiten. Festlegen das folgende Zeilen in der Shell geschrieben werden.

    `config.vm.provision "shell", inline: <<-SHELL`


Neueste Updates herunterladen

    `sudo apt-get update`


Installieren von diversen Diensten
    
    `sudo apt-get install -y \`
    `ca-certificates \`
    `curl \`
    `gnupg \`
    `ufw \`
    `lsb-release`


Verifikation des Dockerimages

    `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor `-o /usr/share/keyrings/docker-archive-keyring.gpg`
    `echo \`
    `"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/`docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \`
    `$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > ``/dev/null`


Firewall Rules setzen
    
    `sudo ufw --force enable`
    `sudo ufw allow 80/tcp`
    `sudo ufw allow 22`
    `sudo ufw allow 2222`


Install Docker

    `sudo apt-get install docker-ce docker-ce-cli containerd.io -y`
    
    
Volume für nginx erstellen und Nginx aktivieren und Port festlegen    
    
    `docker volume create nginx_data`
    `docker run --name some-nginx -d -p 80:80 nginx`


Vagrant Config Ende
    
    `SHELL`
    `end`

### Bestehende VM aus Vagrant-Cloud einrichten
 > [⇧ **Nach oben**](#inhaltsverzeichnis)


```Shell
      $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
``` 
![image](https://user-images.githubusercontent.com/125886136/223113049-a307eba2-46e6-47f5-9c9d-cca056545c13.png)

![image](https://user-images.githubusercontent.com/125886136/223112761-024a1e4f-ba74-472b-be7e-e79650de2b7d.png)


### Funktionsweise getestet inkl. Dokumentation der Testfälle
 > [⇧ **Nach oben**](#inhaltsverzeichnis)

Hier wurde der Vagrantfile von nginx_docker verwendet, weil dadurch die lokale Verbindung über den Docker funktioniert.

#### Testfall für die Funktionalität
 > [⇧ **Nach oben**](#inhaltsverzeichnis)

Um die Funktion zu testen sollte man über den Client mit localhost:100 auf den Linux Server zugreifen können.
Sollte es funktionieren, ist der Reverse-Proxy richtig konfiguriert. <br>
![image](https://user-images.githubusercontent.com/125886136/223134818-3ba1275e-32a0-4f19-a286-c398f3fece2e.png)
<br>
Hier ist ein Curl auf die Webseite.
<br>
![image](https://user-images.githubusercontent.com/125886136/224703243-e7cf1e4b-d97b-47a6-aa86-5955c9156f6e.png)



Damit wir auch sicher sein können, dass der Port über 100 verlauft, wird in dem Beispiel Port 101 verwendet, erwartetes Ergebnis: Keine Verbindung 
<br>
![image](https://user-images.githubusercontent.com/125886136/223134640-c04ce83c-581b-4b9c-8a54-1c33c82d9759.png)


<br>
Tipp: Wurde schon mal über den Browser die Adresse aufgerufen, sollten Sie um fehler zu vermeiden Inkognito Modus verwenden, damit werden die abgespeicherten Cookies nicht verwendet.


### andere, vorgefertige VM auf eigenem Notebook aufgesetzt
 > [⇧ **Nach oben**](#inhaltsverzeichnis)
 
![image](https://user-images.githubusercontent.com/125886136/223118272-71096d8f-a36c-4f81-ab70-b8687d94b7b7.png)
![image](https://user-images.githubusercontent.com/125886136/223118359-b0a3de43-6c6e-4115-9568-f5faa5fbd582.png)
![image](https://user-images.githubusercontent.com/125886136/223118488-5d1ab1a3-5168-4647-9cc8-d4863d7aaeec.png)
![image](https://user-images.githubusercontent.com/125886136/223127351-3b766e6f-3f51-465f-a575-891cce4ee58d.png)
<br>
Hier wird ein vorgefertiger VM auf den Virtualbox aufgesetzt und wird wie im Vagrantfile definiert, werden die Webfiles lokal auch abgespeichert. -> 
* [Vagrantfile von vorgefertiger VM](nginx/Vagrantfile)

### Benutzer- und Rechtevergabe ist eingerichtet
Die Benutzerrechte sind korrekt konfiguriert, unter anderem kann man das durch den Zugriff auf den Ngnix bemerken.
In /etc/passwd wären die Berechtigungen auch ersichtlich.
<br>
![image](https://user-images.githubusercontent.com/125886136/224705203-319e6089-5c20-45a6-956c-abf0198812d5.png)


### Zugang mit SSH-Tunnel abgesichert
Hier wird mit PuTTY getestet, ob eine Verbindung über den Port 2222 forwardet wird auf Port 22 / SSH.
<br>Erwartetes Ergebnis: Verbindung über PuTTY möglich.
<br>Erhaltenes Ergebnis: Verbindung möglich.
<br>
![image](https://user-images.githubusercontent.com/125886136/224702186-5e695f05-0f89-4373-b361-ea42ba9635ce.png)

### Sicherheitsmassnahmen
Um die Sicherheitsaspekt zu garantieren, ist der Root Benutzer deaktiviert und die verschiedenen Berechtigungen für die diversen Benutzern gesetzt.
Um Zugriff auf den Webseite zu erhalten ist der Port auf 100 weitergeleitet worden und die SSH-Verbindung über den Port 2222.

### Vergleich Vorwissen - Wissenszuwachs

+ Verschiedene Arten eine Umgebung zu automatisieren.
+ Vorteil von Automatisierten Skript.
+ Einrichtung über Vagrant.
+ Bedienung von Github.
+ SSH Key vereinfacht erstellen.
+ Verschiedene Sicherheitsaspekte beim Betriebnahme eines Services / Server.
+ Firewallrules erstellen und löschen.
+ Reverse-Proxy einrichten.
+ Docker in Umgebung einbinden und aktivieren.



### Reflexion

#### Tag 1
Heute war eher ein theorätischer Tag. Wir haben viel Informationen erhalten unter anderen, was das Modul beinhaltet und wie es mit der Leistungsbeurteilung aussieht.
Danach konnten wir schon die ersten Erfolgsereignisse erleben. Doch zuvor mussten wir die verschiedenen Applikationen und Clients installieren.
Da ich heute relativ schnell unterwegs war, habe ich mit vagrant angefangen. Ich konnte anhand Vagrant nicht ein Client aufsetzen aber ich konnte manuell aufsetzen.

Ich bin heute ziemlich zufrieden mit meiner Leistung heute.

#### Tag 2
An diesem Tag habe ich mein Problem mit Vagrant analysiert und behoben. Das Problem lag bei der SSH-Privat und Public Key. Ich musste die Schlüsseln nochmals erstellen und in Github & Lab hinterlegen.
Danach habe ich mir den Globalen Vagrant file von Ubuntu gezogen und ausgerollt. Das hat mich sehr gefreut. Dadurch wurde die Motivation noch höher und ich stürzte mich an die nächste Aufgabe. Dort mussten wir viele verschiedene Aufgaben auf Vagrant einrichten. Doch als ich synchronisieren wollte, beschwerte sich Github. Das Problem lag daran, dass der maximaler Filesize überschritten wurde und ich konnte auch nicht die Commits entfernen. Also musste ich mein ganzes Repo löschen und neu aufsetzen.

#### Tag 3
Da ich zu Hause Zeit hatte, habe ich mich an der LB2 gestürzt. Hierbei habe ich zuerst informationen zur Vagrantfile gesammelt um dies zu erstellen. Heute habe ich dann dieses File feingeschliffen und ausgeführt. Jedoch handelte es sich um ein vorgefertigtes File also habe ich für LB2 ein neues erstellt. Dabei verwendete ich Docker Image um nginx zu beziehen. Um den Gastport handelte es sich um Port 80 und der Hostport 100. Damit konnte ich mit Port 100 auf den Server zugreifen von meinem Client aus.

Um das zu bewätigen mussten verschiedene Firewallports freigeschalten werden und auch eingerichtet sein.
Das konnte ich mit dem heutigen Input gut gewältigen.

#### Tag 4
Heute habe ich weiter an meinem Projekt gearbeitet. Zuerst musste ich die Maschine wieder auf die Beine kriegen. Doch das hat nicht wie gewollte funktioniert. Zuerst konnte ich nicht auf die Webseite zugreifen. Mein erster Verdacht lag bei der Servereinstellung. Also habe ich den ganzen Server gelöscht und anhand Vagrant neu aufgesetzt. Doch das Problem war immernoch present.
Dann bemerkte ich, dass die Internetverbindung über WLAN und LAN bestand. Deshalb konnte mein Host den Server nicht sehen. Nachdem ich WLAN entbunden habe, funktionierte es wie gewünscht.
Anschliessend habe ich meine Dokumentation weitergeführt und die verschiedenen Aspekte vom Bewertungsraster anhand eines Testfalls abgedeckt. Unteranderen die Funktionalität von SSH über den Port 2222. Meine Vermutung war, dass es nicht Funktioniert. Aber erstaunlicherweise hat es doch funktioniert. 

