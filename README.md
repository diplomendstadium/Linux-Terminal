```
Erste        .---.
Hilfe       /     \
fürs        \.@-@./
Linux       /`\_/`\
Terminal   //  _  \\
          | \     )|_
Stand:   /`\_`>  <_/ \
15.04.26 \__/'---'\__/


https://github.com/diplomendstadium/Linux-Terminal

# Hilfe zu einzelnen Befehlen
"man befehl" oder oft auch "befehl --help" zeigt Infoseite
hilfreicher ist oft "tldr befehl"

# Tastenkürzel
Strg + L | Leert die Anzeige
Strg + Shift + C | Kopieren
Strg + Shift + V | Einfügen
Tab | Vervollständigt Befehle und Dateinamen, wenn eindeutig
Tab + Tab | zeigt Optionen an, wenn nicht eindeutig
Strg + D | Abmelden
Strg + A | Springt zum Zeilenanfang

# Navigation
pwd | zeigt das aktuelle Arbeitsverzeichnis an
ls | zeigt den Inhalt des aktuellen Verzeichnisses an
  -> "-a" zeigt auch versteckte Inhalte an
  -> "-l" zeigt mehr Infos inkl. Rechte und das Ergebnis als Liste
  -> "-h" zeigt Dateigrößen in lesbaren Einheiten an
  -> für das aktuelle Verzeichnis, sofern nicht anders angegeben
cd Pfad | wechselt in das angegebene Verzeichnis
mkdir ordnername | legt einen ordner an
  -> mkdir -p kann/viele/ordner/erstellen
rmdir ordnername | löscht einen leeren Ordner
mv pfad/datei pfad2/datei2 | verschiebt oder benennt eine Datei um
rm datei | Löscht eine Datei, "rm -r ordner" löscht auch volle Ordner
  -> Vorsicht: Es gibt keinen Papierkorb! "-i" nutzen zur Sicherheit
cp datei1 pfad2/(dateiname) | Kopiert datei1 in Verzeichnis pfad2
  -> "-a" behält Rechte und Zeitstempel bei, -"i" fragt vorher nach
tree | Zeigt übersichtliche Ordnerstrukturen an ("-L 2" beschränkt die
  Anzeigeiefe, "-p" zeigt Reche, "-sh" die Größe)

Absolute Pfadangaben mit "/", also z.B. "/home/ines/bilder/2024/"

Relative Pfadangaben sind möglich. Ist man also z.B. im Ordner "bilder", 
  kann man mit "cd 2024/" in den Ordner wechseln. "." steht bei relativen
  Pfaden für das aktuelle Verzeichnis, ".." für das übergeordnete.
  Aus "2024" kann man also mit "cd ../2023/" ins andere Jahr wechseln.
  "./skript.sh" steht für eine Datei im aktuellen Verzeichnis.
  "~" steht für das Homeverzeichnis der Nutzerin.

# Nützliche Helfer
touch datei | erstellt Datei, falls nicht vorhanden
echo "Hallo Welt" | gibt den Inhalt wieder
cat dateiname | zeigt den Inhalt einer Datei an (-n für Zeilennummern, 
  -E für markiertes Zeilenende)
clear | Löscht die komplette Anzeige des Terminals
su username | Wechselt den Benutzer
sudo befehl | Führt einen Befehl als Administartor aus
sleep 10 | Legt eine Pause ein :)
grep suchmuster Datei | Zeigt nur die Zeilen mit Suchmuster
watch -n 10 -d "date" | führt den Befehl "date" alle 10 Sekunden
    aus und markiert die Differnez zur letzten Ausführung

# Informationen anzeigen
"hostnamectl" oder "uname -a" | Informationen über das System
ip a | aktuelle IP-Adresse anzeigen
last | Zeigt die letzten Anmeldungen
history | Zeigt die Historie der eingegebenen Befehle an
  -> Löschen: Zuerst alle Terminalfenster schließen. Dann entweder
     die Datei "~/.bash_history" löschen oder in einem neuen Fenster
     "history -cw" ausprobieren. Nach Neustart Ergebnis überprüfen!
date | gibt Systemuhrzeit und Datum aus
locale | Zeigt die Ländereinstellungen an
cal | zeigt den aktuellen Kalender
file dateiname | Zeigt den Dateityp an
stat dateiname | Zeigt Infos zur Datei an, z.B. verschiedene Zeitstempel
df -h | Zeigt Speicherverbrauch der Partitionen an
du -hs | Zeigt Größe der Daten im aktuellen Verzeichnis an
free -h | Zeigt freien Speicher an
wc dateiname | Zeigt Zeilen, Worte und Bytes einer Datei an

# Umgang mit Text(dateien)
head dateiname | Gibt nur die ersten 10 Zeilen aus
tail dateiname | Gibt nur die letzten 10 Zeilen aus
more dateiname | Gibt den Inhalt seitenweise aus (vorwärts blättern mit der
  Leertaste, zurück mit "b", beenden mit "q")
cud -d ":" -f 8 dateiname | Zerlegt die Datei nach dem Trennzeichen ":" in
  Einzelteile und zeigt nur das achte Stück an.
tr -s " " | Löscht mehrere Leerzeichen, tr -d " " würde alle löschen
Texteditor "vim dateiname", Tutorial für vim: "vimtutor
expand file | Ersetzt Tabulatoren in der Datei durch Leerzeichen

# Rechte
-(ignorieren) rwx(Besitzer) rw-(Gruppe) r--(alle anderen)
r = lesen | w = schreiben (und löschen) | x = ausführen
u = Besitzer | g = Gruppe | 0 = Andere
chmod u+x file | Gibt Benutzer das Recht auszuführen
chmod go-r file | Entzieht Gruppe und anderen das Recht zu lesen
chmod u=rw,go= file | Benutzer liest und schreibt, Rest hat keine Rechte
(Oder in Zahlen: r=4, w=2, x=1 und dann addieren,
z.B. "chmod 640 file" für -rw-r-----)
chown user:group Verzeichnis | Ändert, wem das Verzeichnis gehört.
Der Benutzer root darf immer alles.
Weitere Informationen hier: https://wiki.ubuntuusers.de/Rechte/

# Klammerexpansion {} und Wildcard *
toch file{01..05}.{txt,docx,pdf} | Erstellt von "file01.txt" bis
  "file05.pdf" alle 15 möglichen Konstellationen
rm file*.txt | Löscht die fünf txt-Dateien wieder

# Umgang mit Variablen
echo "Heute ist $(date +%A)" | Ersetzt Klammerinhalt durch Befehlsergebnis
  Einfache Klammern sorgen dafür, dass die Variable nicht aufgelöst wird!
$_ Arrgument des letzten Befehls (z.B. "mkdir test ; cd $_")
In Skripten: $1 bis $9 Positionsparameter, $0 Skriptname

# Verkettung von Befehlen
 &&  Führt den nächsten Befehl nur aus, wenn es zu keinen Fehlern kam
 ;   Geht auch dann weiter zum nächsten Befehl, wenn es zu Fehlern kam
 >   leitet die Ausgabe des ersten Befehls in Datei um
 >>  wie oben, nur dass angehängt statt überschrieben wird
 |   Leitet Ausgabe des ersten Befehls als Input an zweiten weiter
 ||  Führt 2. Befehl nur aus, wenn erster in Fehler endet

# Paketverwaltung dnf (Fedora, RockyLinux, RedHat, etc.)
dnf search magic | sucht nach Paketen, in denen "magic" vorkommt
dnf upgrade --refresh | sucht und installiert Upgrades
dnf list | Zeigt installierte Pakete
dnf install paketname | Installiert ein Paket
dnf repolist all | zeigt verfügbare Repos
dnf clean all | Löscht Zwischenspeicher
dnf autoremove | Löscht nicht mehr benötigte Pakete
dnf history | Zeigt Bearbeitungshistorie

# Paketverwaltung deb (Debian, LinuxMint, Ubuntu, MXLinux, etc.)
apt update | Aktualisiert die Paketlisen
apt search magic | sucht nach Paketen, in denen "magic" vorkommt
apt show magic-wormhole | Zeigt Infos zu einem konkreten Paket
apt install magic-wormhole | Installiert ein paket
apt remove magic-wormhole | deinstaliert ein Paket
apt upgrade | Updatet sämtliche vorhandenen Pakete
apt autoremove && apt autoclean | Entfernt nicht mehr Nowendiges

# Paketverwaltung mit Flatpaks
Infos zur Einrichtung: https://flathub.org/setup
flatpak search nextcloud | sucht Pakete
flatpak list | zeigt installierete Flatpaks
flatpak upgrade | Sucht und Installiert verfügbare Updates
flatpak install org.torproject.torbrowser-launcher | Installiert Torbrowser
flatpak uninstall org.torproject.torbrowser-launcher | Deinstallation
flatpak history | Zeigt den Verlauf der Aktivitäten

# Benutzerverwaltung
useradd -m username | Erstellt einen neuen Nutzer
passwd username | Vergibt bzw. ändert ein Passwort
passwd -l username | Sperrt User
/etc/passwd (Nutzerübersicht)
  Nutzername:Passwort:UID:GID:Informationen:Homeverzeichnis:LoginShell
/etc/shadow (PasswörterundSicherheit)
  login:passwort:LetztePWÄnderungInTagenSeitJanuar1970:WieLangeMinGültig:
  WieLangeMaxGültig:WieVielTageVorAblaufWarnung:SchonFristNachAblauf:
  UserDeaktiviert
/etc/group (Gruppen)
  Gruppenname:Passwort:gID:MitgliederKommagetrennt
/etc/gshadow (Gruppenpasswörter)
  Gruppenname:Gruppenpasswort:Gruppenverwalter:Mitglieder

# Suchen und Finden
Syntax: find /Verzeichnis/dasdurchsuchtwerden/Soll Attribut
-name "*.txt" sucht genau, -iname hingegen ignoriert Groß-Kleinschreibung
-type f sucht nur reguläre Dateien, -type d ducht nur Ordner
-mtime -3 sucht alles, was in den letzten 3 Tagen verändert wurde
-mtime +7 sucht alles, was nicht in den letzten 7 Tagen verändert wurde

# Umgang mit Laufwerken (Achtug: Hier droht bei Fehlern Datenverlust!)
wipefs /dev/sdc | Formatiert ein Laufwerk
fdisk /dev/sdc | Erstellen von Partitionen
mkfs.xfs /dev/sdc1 | zum Formatieren der Partition
mount /dev/sdc1 /srv/daten | Bindet eine Partition ein
/etc/fstab legt fest, was wie beim Start gemountet wird
  
# Automatisch wiederkehrende Aufgaben (Cron)
Systemweite mit Adminrechten in /etc/crontab eintragen
"systemctl status cron.service" zeigt Cronjobs an
crontab -l zeigt aktuelle Cronjobs des Benutzers
crontab -e editiert die aktuellen cronjobs (https://wiki.ubuntuusers.de/Cron/)
  
# OpenSSL
Dateiverschlüsselung: openssc enc -aes-256-cbc -md sha512 -pbkdf2 -iter 9384 -salt -in dateiname -out dateiname.aes
Entschlüsselung gleich, nur mit zusätzlicher Option "-d" (d für decrypt, hinter ...cbc einfügen)
TextVERschlüsselung: echo "Klartext" | openssl enc -aes-256-cbc -a
TextENTschlüsselung: echo "U2FsdGVkHQ4mf8Ib0=" | openssl enc -aes-256-cbc -a -d

# Textverschlüsselung mit GPG
TextVERschlüsselung: echo "test" | gpg --armor --symmetric --cipher-algo aes256
TextENTschlüsselung: echo "cipher" | gpg --decrypt

# Asymmetrische Crypto mit GPG
Key-Paar erstellen: gpg --full-generate-key (RSA, 4096bit, 2y, Mail leer lassen)
Alle Schlüssel anzeigen: "gpg --list-keys"
Keys exportieren: gpg --output dateiname.key --armor --export keyID
Keys importieren: gpg --import dateiname.key
Fingerprint anzeigen: gpg --fingerprint keyID
Keys signieren: gpg --sign-key keyID
Verschlüsseln: gpg --encrypt --sign --armor -r keyID_Empfänger geheime.datei
Entschlüsseln: gpg --decrypt geheime.datei.gpg > klartext.txt

# Zufallszahlen erzeugen
- openssl rand -hex 99 | tr -dc '0-9'
- gpg --gen-random 16 54 | tr -d "a-f"
- gpg --armor --gen-random 2 300 | tr -d +=/[:alpha:]
- od -vAn -N54 -t u4 < /dev/urandom | tr -d " " | tr -d "\n"
Gleichverteilung prüfen: for i in {0..9}; do grep -o $i zufallszahlen.txt | wc -l; done
In Fünfergruppen sortieren, einfach an einen der Befehel oben anhängen: | fold -w 5 | paste -sd ' '

# Borgbackup
borg init --encryption=repokey /pfad/backup | Neues Backupverz. erzeugen
borg list /pfad/backup | Alle vorhandenen backups anzeigen
borg extract --list /pfad/backup::backupname | Entpackt ein Backup
borg create --list --stats --progress /pfad/backup::{now} ~/Downloads | Erzeugt ein Backup
borg delete --stats --list /pfad/backup::backupname | löscht ein Backup
borg compact --progress --verbose /pfad/backup | Löscht unnötige Daten

# Automatische Transkripte mit Whisper
sudo apt update && sudo apt install -y pipx ffmpeg | Installation vorbereiten
pipx install openai-whisper && pipx ensurepath | Whisper installieren (ohne sudo/root!)
whisper audiofile.mp3 --model turbo --language German > MitZeitstempel.txt | Erstellt Transkript
paste -s -d ' ' transkript.txt > text.txt | Entfernt alle Zeilenumbrüche die Whisper wahllos setzt

# Ollama
Installation: curl -fsSL https://ollama.com/install.sh | sh
Modellübersicht: https://ollama.com/search
ollama run gemma3 "Fasse die wesentlichen Inhalte des folgenden Textes zusammen: $(cat text.txt)"

# YouTube Download mit yt-dlp
Installation: sudo apt install yt-dlp ffmgpeg
Formate anzeigen lassen: yt-dlp --list-formats url
Download: yt-dlp -f a+b mp4 url (a Zahl für Audioformat, b für Video)
Nur Audio: yt-dlp -x --audio-format mp3 url

# Video in Audio umwandeln
ffmpeg -i videodatei.mp4 -vn -q:a 8 audiodatei.mp3

# Audo aufnehmen
ffmpeg -f pulse -i default aufnahme.mp3 (beenden mit q)

# Stop-Motion-Film aus allen Bildern im Ordner erzeugen
ffmpeg -framerate 20 -pattern_type glob -i '*.jpg' -c:v libx264  output.mp4
Für niedrigere Auflösung bzw. kleinere Filmdatei:
ffmpeg -framerate 15 -pattern_type glob -i '*.jpg' -vf "scale=-2:720" -c:v libx264 output.mp4

# Archive
tar cvf archivname.tar DateioderOrdner | Packt angegebene Datei(en) in ein Archiv
tar xvf archivname.tar | Entpackt das Archiv in den aktuellen Ordner

# SSH
ssh-keygen | Erstellt einen eigenen Schlüssel
ssh-copy-id user@host | Kopiert den eigenen Key auf einen Server
Zukünftig ist ein Login ohne Passwort möglich :)

# Dateien via SSH kopieren
scp user@SRC_HOST:/pfad/zur/datei user@DEST_HOST:/pfad/zur/datei
Bei Quelle oder Ziel alles bis inkl. Doppelpunkt weglassen, wenn lokal

# Daten teilen - Python Webserver
python3 -m http.server 1234 | Startet Freigabe des aktuellen Verzeichnisses auf Port 1234
python3 -m http.server -d files/ | Gibt das Verzeichnis files frei auf Port 8000

# Daten teilen - Copyparty
Download: wget https://github.com/9001/copyparty/releases/latest/download/copyparty-sfx.py
Fileserver mit max 1k Daten, der immer 5GB frei lässt und alles nach 1h löscht:
python3 copyparty-sfx.py -sss -v copyparty-files::rwmd:c,lifetime=3600:c,df=5g:c,vmaxn=1k -e2d

# Systempflege
Firmware- & BIOS-Updates, nacheinander: fwupdmgr refresh | fwupdmgr get-updates | fwupdmgr update
Folgende Befehle einfach regelmäßig ausführen.
Den Teil zu den Flatpaks auslassen, falls nicht installiert.
Debian-Basiert: "sudo apt update && sudo apt full-upgrade -y && sudo apt autoclean -y && sudo apt autoremove -y --purge && flatpak update -y"
Ubuntu: "sudo apt update && sudo apt full-upgrade -y && sudo apt autoclean -y && sudo apt autoremove -y --purge && sudo snap refresh && flatpak upgrade -y"
Raspi: "sudo apt update && sudo apt full-upgrade -y && sudo apt autoclean -y && sudo apt autoremove -y --purge && sudo rpi-eeprom-update -d -a"
Fedora/Rocky: "sudo dnf clean all && sudo dnf upgrade --refresh -y && sudo dnf autoremove && flatpak update"
Debian in root: "apt update && apt full-upgrade && apt autoclean && apt autoremove --purge && flatpak update"
Debian als user: "pipx upgrade-all"

# Setup Raspi
Autologin deaktivieren: In der Datei "/etc/lightdm/lightdm.conf" die Zeile "autologin-user=pi" auskommentieren.
Softwareinstallation: sudo apt install -y keepassxc-full kleopatra openssl idle libreoffice thunderbird firefox-l10n-de thunderbird-l10n-de hunspell-de-de gufw onionshare onionshare-cli tree gnome-disk-utility syncthing vim gimp handbrake ffmpeg gnome-text-editor magic-wormhole virt-manager nextcloud-desktop ghostwriter gedit borgbackup python3-full pipx
Firewall einschalten

# Setup Debian 13
In /etc/apt/sources.list überall anpassen zu: "main contrib non-free non-free-firmware"
Zudem als neue Zeile ergänzen: "deb http://deb.debian.org/debian trixie-backports main contrib non-free non-free-firmware"
Als root: "apt update && apt full-upgrade && apt remove evolution && apt install curl ncal borgbackup vim keepassxc torbrowser-launcher vlc ffmpeg pipx nextcloud-desktop python3-full texlive chromium flatpak gnome-software-plugin-flatpak magic-wormhole thunderbird virt-manager && flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo && flatpak install flathub com.prusa3d.PrusaSlicer chat.delta.desktop"
Signal als root installieren: "wget -O- https://updates.signal.org/desktop/apt/keys.asc | gpg --dearmor > signal-desktop-keyring.gpg; cat signal-desktop-keyring.gpg | sudo tee /usr/share/keyrings/signal-desktop-keyring.gpg > /dev/null && wget -O signal-desktop.sources https://updates.signal.org/static/desktop/apt/signal-desktop.sources; cat signal-desktop.sources | sudo tee /etc/apt/sources.list.d/signal-desktop.sources > /dev/null && apt update && apt install signal-desktop"
Als user: "pipx install openai-whisper yt-dlp && pipx ensurepath"

# Setup Linux Mint
sudo apt update && sudo apt full-upgrade && sudo apt remove transmission* libreoffice* hexchat && flatpak install org.onlyoffice.desktopeditors && sudo apt install gnome-clocks keepassxc kleopatra tldr texlive-full python3-full tree openssl vlc torbrowser-launcher vim gimp handbrake ffmpeg magic-wormhole borgbackup chromium 

# Sonstiges
- Optionen zu Befehlen werden in der langversion meist mit "--" angegeben,
  in der Kurzversion mit "-"
- Um Batterie (Kapazität, Ladezyklen, etc.) zu prüfen: 'upower -e' zeigt Geräte inkl. Pfade an, 'upower -i /pfad/zur/battery' zeigt dann Infos zur gewählten Batterie
- 'nohup your_command &' lässt Befehl im Hintergrund laufen, so dass dieser weiterläuft, wenn das Terminal geschlossen wird
- Verstecke Dateien erkennt man in Linux daran, dass deren Dateiname
  mit einem Punkt beginnt.
- Dateiendungen sind eher für den user, das System kommt auch gut ohne aus
- Viele Befehle geben mit der Option "-v" deutlich mehr Rückmeldung
- Ausfühlicher: https://helmbold.de/artikel/Linux-auf-einem-Blatt.pdf
- "#" Kommentar, alles hinter diesem Zeichen wird nicht ausgeführt
- Auf xfs Dateisystemen ist die Dateiwiederherstellung schwieriger...
- Dateinamen dürfen Maximal 255 Zeichen haben
- die Option "-y" bejaht aufkommende Nachfragen
- Deutlich bessere Anleitung: https://github.com/jlevy/the-art-of-command-line
```
