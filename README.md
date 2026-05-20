# Proto2
Allgemeine Erklärung

Der Discord-Minecraft-Bot verbindet einen Discord-Server mit einem Minecraft-Server. Dadurch können beide Plattformen miteinander kommunizieren. Nachrichten aus Discord erscheinen im Minecraft-Chat und Nachrichten aus Minecraft werden automatisch in Discord angezeigt.

Zusätzlich kann der Bot Befehle ausführen, Informationen abrufen und bestimmte Aufgaben automatisieren.

Das System besteht aus mehreren Komponenten, die zusammenarbeiten.

Aufbau des Systems

Das Projekt besteht aus drei Hauptteilen:

Discord-Bot
Minecraft-Bot
Verbindungssystem zwischen beiden Plattformen
1. Discord-Bot – Wie funktioniert er?

Der Discord-Bot läuft dauerhaft im Hintergrund und verbindet sich mit Discord.

Verbindung zu Discord

Der Bot meldet sich mit einem sogenannten Bot-Token bei Discord an.

Beispiel:

client.login(TOKEN)

Das Token funktioniert wie ein Passwort für den Bot.

Nachrichten erkennen

Der Bot überwacht bestimmte Discord-Kanäle.

Sobald jemand eine Nachricht schreibt:

erkennt der Bot die Nachricht
liest den Inhalt
verarbeitet die Daten
sendet sie an Minecraft weiter

Beispiel:

client.on("messageCreate", message => {
})

Dieser Event wird immer ausgelöst, wenn eine neue Nachricht geschrieben wird.

Ideen, die man benutzen kann:
- Zu anderem Spieler(Player-ID) teleportieren mit Befehl
- Gesundheit auffüllen mir Befehl
- Portal mit Befehl öffnen um in eine neue Welt zu kommen
- Tag und Nacht beliebig ändern, Wetter ändern


Node-Red:


Digilab:
Ideen:
- Minecraft-Server mit Digilab verbinden
- Spieler-ID oder Benutzername wird auf dem kleinen Display angezeigt, wenn man stirbt
- LED 1-16 z.B.: 7 Spieler online auf dem Server; 7 LEDs an
- Wenn ein Spieler stirbt, leuchtet die LED bis er respawnt und dann geht das Licht wieder an
- Große LEDs je nach Wetter in verschiedenen Farben: Regen Blau; Sonne Gelb; Nacht Dunkel Blau; Wolken Grau

Dashboard:

