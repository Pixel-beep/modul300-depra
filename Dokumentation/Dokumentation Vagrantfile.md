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
  beispieltext
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
eyJoaXN0b3J5IjpbLTEyMzU1ODc1ODIsLTY0MDM2MTE4NiwtMT
A4Mjc0NjYwLDQ1OTU2NDk4NiwxNzc1NTA2MjIwLDEyNTA0MzYy
OTIsNjg4NjQ5OTQyLDE0MDQyNzUzOTYsLTE2NDkxMjkxNjQsLT
k5MTYzMzg0LC03NTA3MTU5MjJdfQ==
-->