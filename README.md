
# Erste Hilfe fürs Linux Terminal
https://github.com/diplomendstadium/Linux-Terminal

Um diese Datei bei jedem Terminalstart anzuzeigen, einfach im 
Homeverzeichnis speichern und in der Datei ".bashrc" (ebenfalls
im Homeordner) ganz am Ende eine Zeile mit "cat ~/README.md" ergänzen.

[Download](https://github.com/diplomendstadium/Linux-Terminal/raw/main/README.md)

## Hilfe zu einzelnen Befehlen
"man befehl" oder oft auch "befehl --help" zeigt Infoseite

## Tastenkürzel
Strg + L | Leert die Anzeige
Strg + Shift + C | Kopieren
Strg + Shift + V | Einfügen
Tab | Vervollständigt Befehle und Dateinamen, wenn eindeutig
  -> Tab + Tab zeigt Optionen an
Strg + D | Abmelden
Strg + A | Springt zum Zeilenanfang

## Navigation
pwd | zeigt das aktuelle Arbeitsverzeichnis an
ls | zeigt den Inhalt des aktuellen Verzeichnisses an
  -> "-a" zeigt auch versteckte Inhalte an
  -> "-l" zeigt mehr Infos inkl. Rechte und das Ergebnis als Liste
  -> -"h" zeigt Dateigrößen in lesbaren Einheiten an
  -> für das aktuelle Verzeichnis, sofern nicht anders angegeben
cd Pfad | wechselt in das angegebene Verzeichnis
mkdir ordnername | legt einen ordner an
  -> mkdir -p kann/viele/ordner/ineinander/auf/einen/schlag/erstellen
rmdir ordnername | löscht einen leeren Ordner
mv pfad/datei pfad2/datei2 | verschiebt oder benennt eine Datei um
rm datei | Löscht eine Datei, "rm -r ordner" löscht auch volle Ordner
  -> Vorsicht: Es gibt keinen Papierkorb! "-i" nutzen zur Sicherheit
cp datei1 pfad2/(dateiname) | Kopiert datei1 in Verzeichnis pfad2
  -> "-a" behält Rechte und Zeitstempel bei, -"i" fragt vorher nach
tree | Zeigt übersichtliche Ordnerstrukturen an ("-L 2" beschränkt die
  Anzeigeiefe, "-p" zeigt Reche, "-sh" die Größe)

Absolute Pfadangaben beginnen mit "/", also z.B. "/home/ines/bilder/2024/"

Relative Pfadangaben sind möglich. Ist man also z.B. im Ordner "bilder", 
  kann man mit "cd 2024/" in den Ordner wechseln. "." steht bei relativen
  Pfaden für das aktuelle Verzeichnis, ".." für das übergeordnete.
  Aus "2024" kann man also mit "cd ../2023/" ins andere Jahr wechseln.
  "./skript.sh" steht für eine Datei im aktuellen Verzeichnis.
  "~" steht für das Homeverzeichnis der Nutzerin.

## Nützliche Helfer
touch datei | erstellt Datei, falls nicht vorhanden
echo "Hallo Welt" | gibt den Inhalt wieder
cat dateiname | zeigt den Inhalt einer Datei an (-n für Zeilennummern, 
  -E für markiertes Zeilenende)
clear | Löscht die komplette Anzeige des Terminals
su username | Wechselt den Benutzer
sudo befehl | Führt einen Befehl als Administartor aus
sleep 10 | Legt eine Pause ein :)
grep suchmuster Datei | Zeigt nur die Zeilen mit Suchmuster

## Informationen anzeigen
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

## Umgang mit Text(dateien)
head dateiname | Gibt nur die ersten 10 Zeilen aus
tail dateiname | Gibt nur die letzten 10 Zeilen aus
more dateiname | Gibt den Inhalt seitenweise aus (vorwärts blättern mit der
  Leertaste, zurück mit "b", beenden mit "q")
cud -d ":" -f 8 dateiname | Zerlegt die Datei nach dem Trennzeichen ":" in kleine
  und zeigt nur das achte Stück an.
tr -s " " | Löscht mehrere Leerzeichen, tr -d " " würde alle löschen
Texteditor "vim dateiname", Tutorial für vim: "vimtutor
expand file | Ersetzt Tabulatoren in der Datei durch Leerzeichen

## Rechte
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

## Klammerexpansion {} und Wildcard *
toch file{01..05}.{txt,docx,pdf} | Erstellt von "file01.txt" bis
  "file05.pdf" alle 15 möglichen Konstellationen
rm file*.txt | Löscht die fünf txt-Dateien wieder

## Umgang mit Variablen
echo "Heute ist $(date +%A)" | Ersetzt Klammerinhalt durch Befehlsergebnis
  Einfache Klammern sorgen dafür, dass die Variable nicht aufgelöst wird!
$_ Arrgument des letzten Befehls (z.B. "mkdir test ; cd $_")
In Skripten: $1 bis $9 Positionsparameter, $0 Skriptname

## Verkettung von Befehlen
 &&  Führt den nächsten Befehl nur aus, wenn es zu keinen Fehlern kam
 ;   Geht auch dann weiter zum nächsten Befehl, wenn es zu Fehlern kam
 >   leitet die Ausgabe des ersten Befehls in Datei um
 >>  wie oben, nur dass angehängt statt überschrieben wird
 |   Leitet Ausgabe des ersten Befehls als Input an zweiten weiter
 ||  Führt 2. Befehl nur aus, wenn erster in Fehler endet

## Paketverwaltung dnf (Fedora, RockyLinux, RedHat, etc.)
dnf search magic | sucht nach Paketen, in denen "magic" vorkommt
dnf upgrade --refresh | sucht und installiert Upgrades
dnf list | Zeigt installierte Pakete
dnf install paketname | Installiert ein Paket
dnf repolist all | zeigt verfügbare Repos
dnf clean all | Löscht Zwischenspeicher
dnf autoremove | Löscht nicht mehr benötigte Pakete
dnf history | Zeigt Bearbeitungshistorie

## Paketverwaltung deb (Debian, LinuxMint, Ubuntu, MXLinux, etc.)
apt update | Aktualisiert die Paketlisen
apt search magic | sucht nach Paketen, in denen "magic" vorkommt
apt show magic-wormhole | Zeigt Infos zu einem konkreten Paket
apt install magic-wormhole | Installiert ein paket
apt remove magic-wormhole | deinstaliert ein Paket
apt upgrade | Updatet sämtliche vorhandenen Pakete
apt autoremove && apt autoclean | Entfernt nicht mehr Nowendiges

## Paketverwaltung mit Flatpaks
Infos zur Einrichtung: https://flathub.org/setup
flatpak search nextcloud | sucht Pakete
flatpak list | zeigt installierete Flatpaks
flatpak upgrade | Sucht und Installiert verfügbare Updates
flatpak install org.torproject.torbrowser-launcher | Installiert Torbrowser
flatpak uninstall org.torproject.torbrowser-launcher | Deinstallation
flatpak history | Zeigt den Verlauf der Aktivitäten

## Benutzerverwaltung
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

## Suchen und Finden
Syntax: find /Verzeichnis/dasdurchsuchtwerden/Soll Attribut
-name "*.txt" sucht genau, -iname hingegen ignoriert Groß-Kleinschreibung
-type f sucht nur reguläre Dateien, -type d ducht nur Ordner
-mtime -3 sucht alles, was in den letzten 3 Tagen verändert wurde
-mtime +7 sucht alles, was nicht in den letzten 7 Tagen verändert wurde

## Umgang mit Laufwerken (Achtug: Hier droht bei Fehlern Datenverlust!)
wipefs /dev/sdc | Formatiert ein Laufwerk
fdisk /dev/sdc | Erstellen von Partitionen
mkfs.xfs /dev/sdc1 | zum Formatieren der Partition
mount /dev/sdc1 /srv/daten | Bindet eine Partition ein
/etc/fstab legt fest, was wie beim Start gemountet wird

## Systempflege
Folgende Befehle einfach regelmäßig ausführen. Den Teil zu den Flatpaks
  auslassen, falls nicht installiert.
Debian-Basiert: "sudo apt update && sudo apt upgrade -y && 
  sudo apt autoclean -y && sudo apt autoremove -y && flatpak update"
Ubuntu: "sudo apt update && sudo apt upgrade -y && sudo apt 
  autoclean -y && sudo apt autoremove -y && sudo snap refresh &&
  flatpak upgrade"
Raspi: "sudo apt update && sudo apt upgrade -y && sudo apt autoclean -y 
  && sudo apt autoremove -y && sudo rpi-eeprom-update -d -a"
Fedora/Rocky: "sudo dnf clean all && sudo dnf upgrade --refresh -y && 
  sudo dnf autoremove && flatpak update"

## Info
- Optionen zu Befehlen werden in der langversion meist mit "--" angegeben,
  in der Kurzversion mit "-"
- Verstecke Dateien erkennt man in Linux daran, dass deren Dateiname
  mit einem Punkt beginnt.
- Dateiendungen sind eher für den user, das Sysem kommt auch gut ohne aus
- Viele Befehle geben mit der Option "-v" deutlich mehr Rückmeldung
- Ausfühlicher: https://helmbold.de/artikel/Linux-auf-einem-Blatt.pdf
- "#" Kommentar, alles hinter diesem Zeichen wird nicht ausgeführt
- Auf xfs Dateisystemen ist die Dateiwiederherstellung schwieriger...
- Dateinamen dürfen Maximal 255 Zeichen haben
