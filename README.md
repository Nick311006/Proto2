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

Wie dein Node-RED Discord Bot funktioniert
Das große Bild

Minecraft Server Monitor
Aktualisiert automatisch den Discord-Bot wenn Spieler joinen/leaven
Antwortet auf Slash-Commands


Die 3 Trigger (links)

Drei Timestamp-Nodes feuern regelmässig (z.B. alle 30 Sekunden)
Zwei davon fragen den Minecraft-Server ab
Einer initialisiert den Discord-Client


Der Datenfluss
Server Info -> Join/Leave + Last Event

Holt die aktuelle Spielerliste vom Minecraft-Server
Vergleicht sie mit der letzten gespeicherten Liste aus dem Context

Neu drin -> Join-Nachricht wird gebaut
Nicht mehr drin -> Leave-Nachricht wird gebaut


Schickt die Nachrichten an discordMessageManager -> postet in deinen Channel
Speichert nebenbei im flow:

mc_player_list (wer gerade online ist)
mc_last_event (z.B. "Steve joined")



Server Info -> Bot Activity -> Status Storing

Bot Activity liest die Spielerzahl und setzt den Bot-Status auf "Watching X players"
Status Storing parst die Zahl raus und speichert sie als mc_players im flow

Discord Client -> Command Storage

Registriert beim Start die Slash-Commands /ping und /status
Lauscht danach permanent auf interactionCreate-Events

/ping -> antwortet sofort mit "Pong!"
/status -> liest aus dem flow:

mc_players (Spielerzahl)
mc_player_list (wer online ist)
mc_last_event (letztes Ereignis)
Baut daraus eine formatierte Antwort






Der flow-Speicher

Ist das Herzstuck des Ganzen
Die Pipelines laufen unabhangig, teilen sich aber drei Variablen:

mc_players -> aktuelle Spielerzahl
mc_player_list -> genaue Liste wer online ist
mc_last_event -> letztes Ereignis


Nodes schreiben rein, Command-Handler liest daraus

Digilab:
Ideen:
- Minecraft-Server mit Digilab verbinden
- Spieler-ID oder Benutzername wird auf dem kleinen Display angezeigt, wenn man stirbt
- LED 1-16 z.B.: 7 Spieler online auf dem Server; 7 LEDs an
- Wenn ein Spieler stirbt, blinkt die LED bis er respawnt und dann geht das Licht wieder an
- Große LEDs je nach Wetter in verschiedenen Farben: Regen Blau; Sonne Gelb; Nacht Dunkel Blau; Wolken Grau

Dashboard:

Wir haben den Ausgang des Join/Leave Nodes direkt mit einem UI Text Node verbunden. Der Node nimmt dann automatisch den Wert aus msg.payload und zeigt ihn auf dem Dashboard an. Da du mc_last_event bereits als String in der Funktion setzt, kommt der Wert genau so an wie er gespeichert wurde, also z.B. "Steve joined" oder "Steve left".
