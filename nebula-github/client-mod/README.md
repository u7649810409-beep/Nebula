# Nebula Client (Fabric-Mod)

Ingame-Menü im Launcher-Design. **Rechtsshift** öffnet und schließt es.

## Funktionen

- **HUD-Module** (einzeln an/aus): FPS, Koordinaten, Blickrichtung, CPS, Ping, Uhrzeit, Arbeitsspeicher, Tastenanzeige (WASD, Leertaste, Maus)
- **HUD-Editor**: Module mit der Maus an die gewünschte Stelle ziehen (wird in `config/nebula-client.json` gespeichert)
- **Zoom**: Taste **C** gedrückt halten
- **Minispiele**: Pong und Tetris direkt im Spiel
- Alle Tasten lassen sich unter Optionen > Steuerung > „Nebula Client“ ändern

Nicht enthalten sind Funktionen, die einen eigenen Server brauchen (Cosmetics-Shop, Freundesliste, gehostete Welten).

## Bauen

Voraussetzungen: JDK 21 und Gradle 9.2 oder neuer (oder ein Gradle-Wrapper).

```bash
cd client-mod
gradle build
```

Die fertige Datei liegt in `build/libs/nebula-client-1.0.0+mc1.21.11.jar`.
Der Launcher findet sie dort selbst; du kannst sie auch direkt in den Ordner `client-mod/` legen.

Der Launcher kopiert sie beim Start eines **Fabric-Profils mit passender Minecraft-Version** in den Mods-Ordner
und installiert bei Bedarf die Fabric API. Ein/Ausschalten: Einstellungen > „Client-Menü im Spiel“.

## Bauen über GitHub (ohne Gradle auf dem eigenen Rechner)

1. Neues Repository auf github.com anlegen und das ganze Projekt hochladen (inklusive des versteckt wirkenden Ordners `.github`).
2. Im Repository auf **Actions** gehen, den Ablauf „Build Nebula Client“ wählen und **Run workflow** drücken (er startet auch bei jedem Push).
3. Nach ein paar Minuten beim fertigen Lauf unter **Artifacts** „nebula-client“ herunterladen, entpacken und die `.jar` in den Ordner `client-mod/` legen.

## Andere Minecraft-Version

Die Mod ist für **Minecraft 1.21.11** geschrieben (Yarn-Mappings, Java 21). Für eine andere Version die Werte in `gradle.properties`
(`minecraft_version`, `yarn_mappings`, `loader_version`, `fabric_version`, `loom_version`) von https://fabricmc.net/develop übernehmen
und im `fabric.mod.json` die Zeile `"minecraft"` anpassen. Der Code selbst nutzt die Eingabe-API ab 1.21.9
(`Click`, `KeyInput`) und `HudElementRegistry`; für Versionen vor 1.21.9 und ab 26.1 (ohne Mappings, Java 25) muss er angepasst werden.
Der Dateiname enthält die Version (`+mc1.21.11`), daran erkennt der Launcher, für welches Profil die Mod passt.

## Dateien

| Datei | Aufgabe |
| --- | --- |
| `NebulaClient.java` | Einstiegspunkt: Tasten, Zoom, HUD-Hook |
| `NebulaMenuScreen.java` | Das Menü (Module, HUD-Editor, Spiele, Info) |
| `Hud.java`, `HudModule.java` | HUD-Module und ihre Darstellung |
| `Ui.java` | Farben und Zeichenhilfen im Launcher-Stil |
| `PongScreen.java`, `TetrisScreen.java` | Minispiele |
| `Config.java` | Speichern der Einstellungen |
