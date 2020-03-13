Einfacher Webserver mit Ubuntu 16.x.

Erstellen und Starten der VM
Git pull um alle erforderlichen Dateien herunterzuladen.
In das Verzeichnis navigieren und den folgenden Befehl ausführen:
`vagrant up`

Die Dateien werden lokal im aktuellen Verzeichnis abgelegt:
`config.vm.synced_folder ".", "/var/www/html"`

Der Webserver ist unter http://localhost:8080 erreichbar.

`config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true`
Falls dieser Port schon durch ein anderes Programm belegt ist, wird automatisch eine Alternative gewählt.
