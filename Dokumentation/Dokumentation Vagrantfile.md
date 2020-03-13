Vagrantfile Dokumentation
-----------------------------
`Vagrant.configure(2) do |config|`

Die "2" steht für die Version der Objektkonfiguration, die für die Konfiguration dieses Blocks verwendet wird.
Das Objekt kann aber von Version zu Version sehr unterschiedlich sein.

Derzeit gibt es nur zwei unterstützte Versionen: "1" und "2". Version 1 repräsentiert die Konfiguration von Vagrant 1.0.x. "2" repräsentiert die Konfiguration für 1.1+ bis 2.0.x.
Es ist wichtig zu verstehen, dass innerhalb eines einzigen Konfigurationsabschnitts nur eine einzige Version von Vagrant verwendet werden kann.
#
```
config.vm.box = "ubuntu/xenial64"
```
  
  Hier wird festgelegt, welche VM gebraucht wird um die Box zu starten.  Der Wert sollte hier der Name einer installierten Box oder ein Kurzname einer Box in HashiCorps Vagrant Cloud sein.
#
```
config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
```

Hier wird der Port festgelegt über der die Virtuelle Maschine erreichbar ist. In diesem Fall hier wäre das der Port 8080.

Die Option Auto Correct überprüft ob der gesetzte Port mit einem bereits verwendeten Port kollidiert. Wenn ja, wird der Host-Port automatisch geändert. 
 Standardmässig ist diese Option auf "false" gesetzt.
#
 ```
 config.vm.synced_folder ".", "/var/www/html"
```
Synchronisierte Ordner werden innerhalb des Vagrantfiles mit der Methode config.vm.synced_folder konfiguriert. 

Die dazugehörigen Parameter sind folgende:
Der erste Parameter ist ein Pfad zu einem Verzeichnis auf dem Host-Rechner. 
Der zweite Parameter muss ein absoluter Pfad sein, der angibt, wo der Ordner auf dem Gastsystem freigegeben werden soll. Dieser Ordner wird (wenn nötig rekursiv) erstellt, wenn er nicht existiert. 

Standardmässig hängt Vagrant dann die synchronisierten Ordner mit dem Eigentümer/Gruppe an den SSH-Benutzer und alle übergeordneten Ordner an das Stammverzeichnis an.

Man kann bei der Konfiguration synchronisierter Ordner auch zusätzliche optionale Parameter angeben. Diese Optionen sind unten aufgeführt. 
Zusätzlich zu diesen Optionen kann der spezifische synchronisierte Ordnertyp weitere Optionen zulassen:

*- `create` Wenn true, wird der Host-Pfad erstellt, wenn er nicht existiert. Standardeinstellung: falsch.*

*- `disabled` Wenn true, wird dieser synchronisierte Ordner deaktiviert und nicht eingerichtet. 
Dies kann verwendet werden, um einen zuvor definierten synchronisierten Ordner zu deaktivieren oder um eine Definition auf der Grundlage eines externen Faktors bedingt zu deaktivieren.*

*- `group`  Die Gruppe, der der synchronisierte Ordner gehören wird. Standardmäßig wird dies der SSH-Benutzer sein. Einige synchronisierte Ordnertypen unterstützen die Änderung der Gruppe nicht.*

*- `mount_options`  Eine Liste zusätzlicher Einhängeoptionen, die an den Einhängebefehl übergeben werden.*

*- `owner` Der Benutzer, der der Eigentümer dieses synchronisierten Ordners sein sollte. Standardmäßig wird dies der SSH-Benutzer sein. Einige synchronisierte Ordnertypen unterstützen die Änderung des Eigentümers nicht.*

*- `type`  Der Typ des synchronisierten Ordners. Wenn dies nicht angegeben wird, wählt Vagrant automatisch die beste synchronisierte Ordneroption für Ihre Umgebung. Andernfalls können Sie einen bestimmten Typ wie "nfs" angeben.*

*- `id` Der Name für den Mount-Point dieses synchronisierten Ordners auf dem Gastcomputer. Dieser wird angezeigt, wenn man den Mount auf dem Gastsystem ausführt.*

  #
 ```
config.vm.provider "virtualbox" do |vb|
```
Der config.vm.provider Befehl ist sehr simpel, es nimmt nur einen einzigen Parameter: den Namen des zu konfigurierenden Providers. Dann wird ein innerer Block mit benutzerdefinierten Konfigurationsoptionen angezeigt, der zur Konfiguration dieses Providers verwendet werden kann.

Diese innere Konfiguration unterscheidet sich von Anbieter zu Anbieter.
Einige Anbieter wie zum Beispiel VirtualBox brauchen keine anbieterspezifische Konfiguration sonder funktionieren "out of the box".
Laut dem offiziellem Wiki Artikel von Vagrant, ist die anbieterspezifische Konfiguration als eine Möglichkeit gedacht, mehr Optionen bereitzustellen, um den Wunsch-Anbieter optimal zu nutzen. Sie ist nicht als Hindernis gedacht, gegen einen bestimmten Anbieter anzutreten.

Vorrangige Konfiguration
Man kann auch nicht-anbieter-spezifische Konfigurationen wie config.vm.box und jede andere Vagrant-Konfiguration außer Kraft setzen. Dies geschieht durch die Angabe eines zweiten Arguments an config.vm.provider. 
In unserem Fall ist der festgelegte Anbieter Virtualbox. Mit den Paramterangaben "do |vb|" wird alles überschrieben und Virtualbox für dieses Vagrantfile als Anbieter gesetzt.
#
```
  vb.memory = "512"
  ```

Mit dieser Angabe wird der Arbeitsspeicher für die Maschine festgelegt.
Man könnte auch die CPU Kerne festlegen, mit folgender Konfiguration

  `v.cpus = 2`
#
```
config.vm.provision "shell", inline: <<-SHELL
  sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
  sudo apt-get update
  sudo apt-get -y install apache2 
SHELL
end
```
`config.vm.provision "shell", inline: <<-SHELL`
Gibt einen Shell-Befehl an, der inline auf dem entfernten Rechner ausgeführt werden soll.
`sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main `
Mit diesem Befehl wird dasUbuntu Package von einem Debian Mirror-Archiv geholt

#
```
title: Dokumentation eines Vagrantfiles M300 LB 2
author: Marc De Pra
date: 13.03.2020
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA3ODgzMzE0OCwtNzIwMTMwMzUsLTEyMz
U1ODc1ODIsLTY0MDM2MTE4NiwtMTA4Mjc0NjYwLDQ1OTU2NDk4
NiwxNzc1NTA2MjIwLDEyNTA0MzYyOTIsNjg4NjQ5OTQyLDE0MD
QyNzUzOTYsLTE2NDkxMjkxNjQsLTk5MTYzMzg0LC03NTA3MTU5
MjJdfQ==
-->