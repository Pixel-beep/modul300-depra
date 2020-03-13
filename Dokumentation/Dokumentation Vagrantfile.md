Vagrantfile Dokumentation
-----------------------------
`Vagrant.configure(2) do |config|`

Die "2" steht für die Version der Objektkonfiguration, die für die Konfiguration dieses Blocks verwendet wird.
Das Objekt kann aber von Version zu Version sehr unterschiedlich sein.

Derzeit gibt es nur zwei unterstützte Versionen: "1" und "2". Version 1 repräsentiert die Konfiguration von Vagrant 1.0.x. "2" repräsentiert die Konfiguration für 1.1+ bis 2.0.x.
Es ist wichtig zu verstehen, dass innerhalb eines einzigen Konfigurationsabschnitts nur eine einzige Version von Vagrant verwendet werden kann.
#
`config.vm.box = "ubuntu/xenial64"`
  
  Hier wird spezifiziert welche VM Box verwendet werden soll.
#
  `config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true`

Hier wird der Port festgelegt über der die Virtuelle Maschine erreichbar ist. In diesem Fall hier wäre das der Port 8080.

Die Option Auto Correct überprüft ob der gesetzte Port mit einem bereits verwendeten Port kollidiert. Wenn ja, wird der Host-Port automatisch geändert. 
 Standardmässig ist diese Option auf "false" gesetzt.
#
 `config.vm.synced_folder ".", "/var/www/html"`

Synchronisierte Ordner werden innerhalb des Vagrantfiles mit der Methode config.vm.synced_folder konfiguriert. 

Die Verwendung der Konfigurationsanweisung ist sehr einfach:
Der erste Parameter ist ein Pfad zu einem Verzeichnis auf dem Host-Rechner. Wenn der Pfad relativ ist, ist er relativ zur Projekt-Wurzel. Der zweite Parameter muss ein absoluter Pfad sein, der angibt, wo der Ordner auf dem Gastsystem freigegeben werden soll. Dieser Ordner wird (wenn nötig rekursiv) erstellt, wenn er nicht existiert. Standardmäßig hängt Vagrant die synchronisierten Ordner mit dem Eigentümer/Gruppe an den SSH-Benutzer und alle übergeordneten Ordner an das Stammverzeichnis an.

Sie können bei der Konfiguration synchronisierter Ordner auch zusätzliche optionale Parameter angeben. Diese Optionen sind unten aufgeführt. Ausführlichere Beispiele für die Verwendung einiger dieser Optionen werden im Anschluss an diesen Abschnitt gezeigt. Beachten Sie, dass das Eigentümer/Gruppen-Beispiel zwei zusätzliche, durch Kommata getrennte Optionen enthält.
Zusätzlich zu diesen Optionen kann der spezifische synchronisierte Ordnertyp weitere Optionen zulassen. Weitere Einzelheiten finden Sie in der Dokumentation für Ihren spezifischen synchronisierten Ordnertyp. Die eingebauten synchronisierten Ordnertypen sind auf anderen Seiten dokumentiert, die in der Navigation für diese Dokumente verfügbar sind.
- create (boolean) - Wenn true, wird der Host-Pfad erstellt, wenn er nicht existiert. Standardeinstellung: falsch.
- disabled (boolean) - Wenn true, wird dieser synchronisierte Ordner deaktiviert und nicht eingerichtet. Dies kann verwendet werden, um einen zuvor definierten synchronisierten Ordner zu deaktivieren oder um eine Definition auf der Grundlage eines externen Faktors bedingt zu deaktivieren.
- group (string) - Die Gruppe, der der synchronisierte Ordner gehören wird. Standardmäßig wird dies der SSH-Benutzer sein. Einige synchronisierte Ordnertypen unterstützen die Änderung der Gruppe nicht.
- mount_options (array) - Eine Liste zusätzlicher Einhängeoptionen, die an den Einhängebefehl übergeben werden.
- owner (string) - Der Benutzer, der der Eigentümer dieses synchronisierten Ordners sein sollte. Standardmäßig wird dies der SSH-Benutzer sein. Einige synchronisierte Ordnertypen unterstützen die Änderung des Eigentümers nicht.
- type (string) - Der Typ des synchronisierten Ordners. Wenn dies nicht angegeben wird, wählt Vagrant automatisch die beste synchronisierte Ordneroption für Ihre Umgebung. Andernfalls können Sie einen bestimmten Typ wie "nfs" angeben.
- id (string) - Der Name für den Mount-Point dieses synchronisierten Ordners auf dem Gastcomputer. Dieser wird angezeigt, wenn Sie das Mount auf dem Gastsystem ausführen.
Synchronisierte Ordner werden automatisch während des Vagabundierens und des Vagabundierens des Neuladens eingerichtet.
Synchronisierte Ordner können durch Hinzufügen der Option "Deaktiviert" zu jeder Definition deaktiviert werden:

  #
`config.vm.provider "virtualbox" do |vb|
  vb.memory = "512"`
end
Text
#
`config.vm.provision "shell", inline: <<-SHELL`
  Packages vom lokalen Server holen
  `sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
  sudo apt-get update
  sudo apt-get -y install apache2 
SHELL
end`

#

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NDI4ODIzNjAsLTEyMzU1ODc1ODIsLT
Y0MDM2MTE4NiwtMTA4Mjc0NjYwLDQ1OTU2NDk4NiwxNzc1NTA2
MjIwLDEyNTA0MzYyOTIsNjg4NjQ5OTQyLDE0MDQyNzUzOTYsLT
E2NDkxMjkxNjQsLTk5MTYzMzg0LC03NTA3MTU5MjJdfQ==
-->