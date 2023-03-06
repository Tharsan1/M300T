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
  - [Einführung](#einführung)
    - [Git einrichten](#git-einrichten)
  - [Markdown](#markdown)
  - [Umgebung auf eigenem Notebook eingerichtet und funktionsfähig](#umgebung-auf-eigenem-notebook-eingerichtet-und-funktionsfähig)
    - [VirtualBox](#virtualbox)
    - [Visualstudio-Code](#visualstudio-code)
    - [Git-Client](#git-client)
    - [SSH-Key für Client erstellt](#ssh-key-für-client-erstellt)
  - [Vagrant](#vagrant)
    - [Befehle](#befehle)
    - [Eingerichtete Umgebung - Dokumentierung Code](#eingerichtete-umgebung---dokumentierung-code)
  - [Eigene Lernumgebung (PLE) ist eingerichtet](#eigene-lernumgebung-ple-ist-eingerichtet)
    - [GitHUB oder Gitlab-Account ist erstellt](#github-oder-gitlab-account-ist-erstellt)
    - [Git-Client wurde verwendet](#git-client-wurde-verwendet)
    - [Bestehende VM aus Vagrant-Cloud einrichten](#bestehende-vm-aus-vagrant-cloud-einrichten)
    - [Funktionsweise getestet inkl. Dokumentation der Testfälle](#funktionsweise-getestet-inkl-dokumentation-der-testfälle)
      - [Testfall für die Funktionalität](#testfall-für-die-funktionalität)
    - [andere, vorgefertige VM auf eigenem Notebook aufgesetzt](#andere-vorgefertige-vm-auf-eigenem-notebook-aufgesetzt)
  - [Sicherheitsaspekte sind implementiert](#sicherheitsaspekte-sind-implementiert)
    - [Firewall eingerichtet inkl. Rules](#firewall-eingerichtet-inkl-rules)
    - [Reverse-Proxy eingerichtet](#reverse-proxy-eingerichtet)
    - [Benutzer- und Rechtevergabe ist eingerichtet](#benutzer--und-rechtevergabe-ist-eingerichtet)
    - [Zugang mit SSH-Tunnel abgesichert](#zugang-mit-ssh-tunnel-abgesichert)
    - [Sicherheitsmassnahmen sind dokumentiert](#sicherheitsmassnahmen-sind-dokumentiert)
    - [Projekt mit Git und Mark Down dokumentiert](#projekt-mit-git-und-mark-down-dokumentiert)
  - [Zusätzliche Bewertungspunkte](#zusätzliche-bewertungspunkte)
    - [Kreativität](#kreativität)
    - [Komplexität](#komplexität)
    - [Umfang](#umfang)
    - [Cloud-Integration](#cloud-integration)
    - [Authentifizierung und Autorisierung via LDAP](#authentifizierung-und-autorisierung-via-ldap)
    - [Übungsdokumentation als Vorlage für Modul-Unterlagen erstellt](#übungsdokumentation-als-vorlage-für-modul-unterlagen-erstellt)
    - [Vergleich Vorwissen - Wissenszuwachs](#vergleich-vorwissen---wissenszuwachs)
    - [Reflexion](#reflexion)
      - [Tag 1](#tag-1)
      - [Tag 2](#tag-2)
      - [Tag 3](#tag-3)

 > [⇧ **Nach oben**](#inhaltsverzeichnis)
 ## Einführung
 Als erstens wird eine kleine Einführung über alle wichtigen Services stehen.
 
 > [⇧ **Nach oben**](#inhaltsverzeichnis)
 ### Git einrichten
 ```
 git config --global user.name "username"
 git config --global user.email "E-Mail"
 ```
 
 > [⇧ **Nach oben**](#inhaltsverzeichnis)
 ## Markdown
 Markdown bearbeiten in Code:
 https://code.visualstudio.com/docs/languages/markdown
 
 Markdown wird zum Darstelle einer Datei gebraucht in einem "Human Stil".
 <br>
 
\# H1 Übertitel 1 <br>
\## H2 Übertitel 2 <br>
\### H3 Übertitel 3 <br>
\#### H4 Übertitel 4 <br>
\##### H5 Übertitel 5 <br>
\###### H6 Übertitel 6 <br>
<br>
\Alternatively, for H1 and H2, an underline-ish style: <br>

<p> \Alt-H1 <br>
\====== </p>
<br>
<p> \Alt-H2 <br>
\------ </p>
<br>

> [⇧ **Nach oben**](#inhaltsverzeichnis)
## Umgebung auf eigenem Notebook eingerichtet und funktionsfähig

<a name="virtualbox"></a>
### VirtualBox
![image](https://user-images.githubusercontent.com/125886136/221586873-69d2dcf5-e1c1-47c1-ac1b-5f71bebd8b6b.png)

<a name="visualstudio-code"></a>
### Visualstudio-Code
![image](https://user-images.githubusercontent.com/125886136/221587138-2c3fcb92-6e7d-4804-bd68-b0e10cffaf40.png)

<a name="git-client"></a>
### Git-Client
![image](https://user-images.githubusercontent.com/125886136/221587230-4be1faa4-1b76-44b0-8d56-470aada72441.png)

<a name="ssh-key-für-client-erstellt"></a>
### SSH-Key für Client erstellt
![image](https://user-images.githubusercontent.com/125886136/221587370-1de9481e-30bd-454f-9f0b-0c43d2a16db1.png)

<a name="vagrant"></a>
## Vagrant
Vagrant ist eine freie Ruby-Anwendung zum Erstellen und Verwalten virtueller Maschinen.[2] Vagrant ermöglicht einfache Softwareverteilung (englisch Deployment) insbesondere in der Software- und Webentwicklung und dient als Wrapper zwischen Virtualisierungssoftware wie VirtualBox, KVM/QEMU, VMware und Hyper-V und Software-Configuration-Management-Anwendungen beziehungsweise Systemkonfigurationswerkzeugen wie Chef, Saltstack und Puppet.

![image](https://user-images.githubusercontent.com/125886136/221587053-63c267aa-be05-4716-a107-02648a029add.png)

<a name="befehle"></a>
### Befehle
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

<a name="eingerichtete-umgebung---dokumentierung-code"></a>

### Eingerichtete Umgebung - Dokumentierung Code
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

<a name="eigene-lernumgebung-ple-ist-eingerichtet"></a>

## Eigene Lernumgebung (PLE) ist eingerichtet

<a name="github-oder-gitlab-account-ist-erstellt"></a>

### GitHUB oder Gitlab-Account ist erstellt
![image](https://user-images.githubusercontent.com/125886136/221588927-e48ec643-ca30-4781-95fa-c1e819dd9c35.png)

<a name="git-client-wurde-verwendet"></a>

### Git-Client wurde verwendet
![image](https://user-images.githubusercontent.com/125886136/221588992-729d10e0-b178-4b7e-a928-a2be927322ea.png)

<br>

<a name="bestehende-vm-aus-vagrant-cloud-einrichten"></a>

### Bestehende VM aus Vagrant-Cloud einrichten

```Shell
      $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
``` 
![image](https://user-images.githubusercontent.com/125886136/223113049-a307eba2-46e6-47f5-9c9d-cca056545c13.png)

![image](https://user-images.githubusercontent.com/125886136/223112761-024a1e4f-ba74-472b-be7e-e79650de2b7d.png)

<a name="funktionsweise-getestet-inkl-dokumentation-der-testfälle"></a>

### Funktionsweise getestet inkl. Dokumentation der Testfälle
Hier wurde der Vagrantfile von nginx_docker verwendet, weil dadurch die lokale Verbindung über den Docker funktioniert.

<a name="testfall-für-die-funktionalität"></a>

#### Testfall für die Funktionalität
Um die Funktion zu testen sollte man über den Client mit localhost:100 auf den Linux Server zugreifen können.
![image](https://user-images.githubusercontent.com/125886136/223134818-3ba1275e-32a0-4f19-a286-c398f3fece2e.png)


Damit wir auch sicher sein können, dass der Port über 100 verlauft, wird in dem Beispiel Port 101 verwendet, erwartetes Ergebnis: Keine Verbindung 
<br>
![image](https://user-images.githubusercontent.com/125886136/223134640-c04ce83c-581b-4b9c-8a54-1c33c82d9759.png)


<br>
Tipp: Wurde schon mal über den Browser die Adresse aufgerufen, sollten Sie um fehler zu vermeiden Inkognito Modus verwenden, damit werden die abgespeicherten Cookies nicht verwendet.

<a name="andere-vorgefertige-vm-auf-eigenem-notebook-aufgesetzt"></a>

### andere, vorgefertige VM auf eigenem Notebook aufgesetzt
![image](https://user-images.githubusercontent.com/125886136/223118272-71096d8f-a36c-4f81-ab70-b8687d94b7b7.png)
![image](https://user-images.githubusercontent.com/125886136/223118359-b0a3de43-6c6e-4115-9568-f5faa5fbd582.png)
![image](https://user-images.githubusercontent.com/125886136/223118488-5d1ab1a3-5168-4647-9cc8-d4863d7aaeec.png)
![image](https://user-images.githubusercontent.com/125886136/223127351-3b766e6f-3f51-465f-a575-891cce4ee58d.png)
<br>
Hier wird ein vorgefertiger VM auf den Virtualbox aufgesetzt und wird wie im Vagrantfile definiert, werden die Webfiles lokal auch abgespeichert. -> 
* [Vagrantfile von vorgefertiger VM](nginx/Vagrantfile)

## Sicherheitsaspekte sind implementiert

### Firewall eingerichtet inkl. Rules

### Reverse-Proxy eingerichtet

### Benutzer- und Rechtevergabe ist eingerichtet

### Zugang mit SSH-Tunnel abgesichert

### Sicherheitsmassnahmen sind dokumentiert

### Projekt mit Git und Mark Down dokumentiert

<br>
<br>

## Zusätzliche Bewertungspunkte

### Kreativität

### Komplexität

### Umfang

### Cloud-Integration

### Authentifizierung und Autorisierung via LDAP

### Übungsdokumentation als Vorlage für Modul-Unterlagen erstellt

### Vergleich Vorwissen - Wissenszuwachs

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

