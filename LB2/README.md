# M300 Leistungsbeurteilung 2
Plattformübergreifende Dienste in ein Netzwerk integrieren

## Autor
Tharsan Pethurupillai

## Inhaltsverzeichnis

- [Einführung](#einfuehrung)
  - [Git einrichten](#giteinrichten)
- [Markdown](#markdown)
- [Software einrichten](#softwareeinrichten)
  - [VirtualBox einrichten](#virtualboxeinrichten)
  - [Vagrant einrichten](#vagranteinrichten)
  - [Visualstudio-Code einrichten](#visualstudiocodeeinrichten)
  - [Git-Client einrichten](#gitclienteinrichten)
  - [SSH-Key für Client erstellt](#sshkeyerstellen)
- [Vagrant](#vagrant)
  - [Befehle](#Befehle)
  - [Eingerichtete Umgebung - Dokumentierung Code](#code)

 <a bane="einfuehrung"></a>
 ##Einführung
 Als erstens wird eine kleine Einführung über alle wichtigen Services stehen.
 
 <a name="giteinrichten"></a>
 ### Git einrichten
 ```
 git config --global user.name "username"
 git config --global user.email "E-Mail"
 ```
 
 <a name="markdown"></a>
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

<a name="softwareeinrichten"></a>
## Umgebung auf eigenem Notebook eingerichtet und funktionsfähig

<a name="virtualboxeinrichten"></a>
### VirtualBox
![image](https://user-images.githubusercontent.com/125886136/221586873-69d2dcf5-e1c1-47c1-ac1b-5f71bebd8b6b.png)

<a name="vagranteinrichten"></a>
### Vagrant
![image](https://user-images.githubusercontent.com/125886136/221587053-63c267aa-be05-4716-a107-02648a029add.png)

<a name="visualstudiocodeeinrichten"></a>
### Visualstudio-Code
![image](https://user-images.githubusercontent.com/125886136/221587138-2c3fcb92-6e7d-4804-bd68-b0e10cffaf40.png)

<a name="gitclienteinrichten"></a>
### Git-Client
![image](https://user-images.githubusercontent.com/125886136/221587230-4be1faa4-1b76-44b0-8d56-470aada72441.png)

<a name="sshkeyerstellen"></a>
### SSH-Key für Client erstellt
![image](https://user-images.githubusercontent.com/125886136/221587370-1de9481e-30bd-454f-9f0b-0c43d2a16db1.png)

<a name="vagrant"></a>
## Vagrant
Vagrant ist eine freie Ruby-Anwendung zum Erstellen und Verwalten virtueller Maschinen.[2] Vagrant ermöglicht einfache Softwareverteilung (englisch Deployment) insbesondere in der Software- und Webentwicklung und dient als Wrapper zwischen Virtualisierungssoftware wie VirtualBox, KVM/QEMU, VMware und Hyper-V und Software-Configuration-Management-Anwendungen beziehungsweise Systemkonfigurationswerkzeugen wie Chef, Saltstack und Puppet.

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

<a name="code"></a>
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


VM Config einleiten. Festlegen das folgende zeilen in der Shell geschrieben werden.

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


Firewall Rules setzten
    
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

## Eigene Lernumgebung (PLE) ist eingerichtet
### GitHUB oder Gitlab-Account ist erstellt
![image](https://user-images.githubusercontent.com/125886136/221588927-e48ec643-ca30-4781-95fa-c1e819dd9c35.png)

### Git-Client wurde verwendet
![image](https://user-images.githubusercontent.com/125886136/221588992-729d10e0-b178-4b7e-a928-a2be927322ea.png)

### Dokumentation ist als Mark Down vorhanden
Dieses Dokumentation wurde mit Mark Down erstellt.

### Mark down-Editor ausgewählt und eingerichtet
Für Mark down-Editor wurde Visual Studio Code verwendet.

### Mark down ist strukturiert
Es ist strukturiert.

### Persönlicher Wissenstand im Bezug auf die wichtigsten Themen sind dokumentiert
Siehe bei den jeweiligen Abschnitten.

### Wichtige Lernschritte sind dokumentiert
Siehe bei den jeweiligen Abschnitten.

<br>
<br>

## Vagrants

### Bestehende VM aus Vagrant-Cloud einrichten

```Shell
      $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
``` 
![image](https://user-images.githubusercontent.com/125886136/223113049-a307eba2-46e6-47f5-9c9d-cca056545c13.png)

![image](https://user-images.githubusercontent.com/125886136/223112761-024a1e4f-ba74-472b-be7e-e79650de2b7d.png)


### Funktionsweise getestet inkl. Dokumentation der Testfälle
Hier wurde der Vagrantfile von nginx_docker verwendet, weil dadurch die lokale Verbindung über den Docker funktioniert.

#### Testfall für die Funktionalität:
Um die Funktion zu testen sollte man über den Client mit localhost:100 auf den Linux Server zugreifen können.
![image](https://user-images.githubusercontent.com/125886136/223134818-3ba1275e-32a0-4f19-a286-c398f3fece2e.png)


Damit wir auch sicher sein können, dass der Port über 100 verlauft, wird in dem Beispiel Port 101 verwendet, erwartetes Ergebnis: Keine Verbindung 
<br>
![image](https://user-images.githubusercontent.com/125886136/223134640-c04ce83c-581b-4b9c-8a54-1c33c82d9759.png)


<br>
Tipp: Wurde schon mal über den Browser die Adresse aufgerufen, sollten Sie um fehler zu vermeiden Inkognito Modus verwenden, damit werden die abgespeicherten Cookies nicht verwendet.

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


