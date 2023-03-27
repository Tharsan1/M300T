<a name="m300-leistungsbeurteilung-2"></a>
# M300 Leistungsbeurteilung 3
Plattformübergreifende Dienste in ein Netzwerk integrieren

<a name="autor"></a>
## Autor
Tharsan Pethurupillai

<a name="inhaltsverzeichnis"></a>
## Inhaltsverzeichnis

- [M300 Leistungsbeurteilung 3](#m300-leistungsbeurteilung-3)
  - [Autor](#autor)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
  - [Docker](#docker)
    - [Befehle](#befehle)
    - [Netzwerkplan](#netzwerkplan)
    - [Webserver erstellen](#webserver-erstellen)
      - [Dockerfile](#dockerfile)
      - [Container starten](#container-starten)
    - [Service Überwachung](#service-überwachung)
    - [Container Sicherheit](#container-sicherheit)
      - [Read-Only](#read-only)
    - [Vergleich Vorwissen - Wissenszuwachs](#vergleich-vorwissen---wissenszuwachs)
    - [Reflexion](#reflexion)
      - [Tag 5](#tag-5)
      - [Tag 6](#tag-6)
      - [Tag 7](#tag-7)

## Docker
Docker ist eine Freie Software zur Isolierung von Anwendungen mit Hilfe von Containervirtualisierung. Docker vereinfacht die Bereitstellung von Anwendungen, weil sich Container, die alle nötigen Pakete enthalten, leicht als Dateien transportieren und installieren lassen.

### Befehle

| Befehl            | Funktion                                             |
| -------------     | ---------------------------------------------------- | 
| ```docker pull```      | Holt ein Image. |
| ```docker run```      | Started VM mit dem ausgewähltem Image. |
| ```docker ps```      | Zeigt laufende Maschinen. |
| ```docker version```      | Zeigt die Docker Version von Echo-Client und Server an. |
| ```docker images```        | Listet alle Docker Images auf. |
| ```docker exec```       | Führt einen Befehl in einem laufenden Container aus. |
| ```docker search```    | Durchsucht das Docker Hub nach Images. |
| ```docker attach```      | Hängt etwas an einen laufenden Container an. |
| ```docker commit```   | Erstellt ein neues Image mit den Änderungen, die an einem Container vorgenommen worden sind. |
| ```docker stop```   | Haltet die gewünschte Maschine an. |

### Netzwerkplan

### Webserver erstellen
Hier wird kurz erklärt wie man eine einfache Webseite anhand eines Containers anbietet.

#### Dockerfile
```
#
#	Einfache Apache Umgebung
#
FROM ubuntu:14.04
RUN apt-get update
RUN apt-get -q -y install apache2 
# Konfiguration Apache
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
RUN mkdir -p /var/lock/apache2 /var/run/apache2
EXPOSE 80
VOLUME /var/www/html
CMD /bin/bash -c "source /etc/apache2/envvars && exec /usr/sbin/apache2 -DFOREGROUND"
```

#### Container starten
Zuerst Image erstellen:
```
docker build C:\Users\Thars\M300T\LB3\dockerfile
```

Danach Image umbennen, damit es einfacher zu erkennen ist:
``` 
docker tag <ID> apache2
```

Nun kann man die VM starten (hier wird der Port 8080 weitergeleitet):
```
docker run --rm -d -p 8080:80 -v web:/var/www/html --name apache2 <ID>
```

So könnte man im nachhinein auf die Shell zugreifen (Beachten, dass winpty benutzt wird):
```
winpty docker exec -it apache2 bash
```

So könnte man auch die Webseite abändern:
```
docker cp C:\Users\Thars\M300T\LB3\index.html apache2:/var/www/html/
```
### Service Überwachung
Dieser Service ist sehr einfach einzurichten:
```
run -d --name cadvisor -v /:/rootfs:ro -v /var/run:/var/run:rw -v /sys:/sys:ro -v /var/lib/docker/:/var/lib/docker:ro -p 8080:8080 google/cadvisor:latest
```
Somit kann man nun im Browser mit "localhost:8080" auf den Service zugreifen.

### Container Sicherheit
Hiermit kann der normale User keine sudo Befehle ausführen.
Das Dockerfile muss folgendes beinhalten:
```
RUN useradd -ms /bin/bash Username
USER Username
WORKDIR /homedir
```

#### Read-Only
Wenn man den Docker mit der Option read-only startet, können keine Änderungen am Dateisystem vorgenommen werden (auch mit sudo nicht):
```
docker run --read-only -d -t --name apache2 Image
```

### Vergleich Vorwissen - Wissenszuwachs

+ 


### Reflexion

#### Tag 5
Heute habe ich mich mit dem Docker Theorie befasst und anschliessend ausgetestet. Dafür musste ich zuerst Docker auf meinem Laptop installieren, aber Docker verursachte viele Probleme. Ich musste Docker erst deinstallieren danach wieder installieren. Leider hat das sehr viel an Zeit gekostet. Danach konnte ich die verschiedenen Befehle ausprobieren. Die Befehle an sich waren sehr einfach definiert und waren einfach zu merken. Als ich dann auf die Uhr schaute war der Nachmittag schon vorbei.


#### Tag 6


#### Tag 7

