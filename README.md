# 🏠✨ Smarvy Area Card (v5.0.1)

Die **Smarvy Area Card** ist eine Premium-Raumkarte für Home Assistant. Sie kombiniert modernes **Glassmorphism-Design** mit intuitiven Touch-Gesten, dynamischen Pop-ups und einem innovativen „Progress Veil“ (Lade-Schleier beim Gedrückthalten). 

Perfekt geeignet, um ganze Räume (Areas) auf einen Blick zu überwachen und zu steuern, ohne viel Platz auf deinem Dashboard zu verbrauchen.

---

## ✨ Highlights & Features

* 💎 **Premium Glassmorphism:** Schicke Milchglas-Optik, die sich fließend in deine Dashboard-Hintergründe einfügt (inklusive "Dark Text"-Modus für helle Hintergründe).
* 🎛️ **Squircle Master Button:** Der Haupt-Button sieht nicht nur modern aus, sondern dient als "Master Off"-Schalter. Langes Drücken schaltet alle aktiven Lichter, Schalter und Ventilatoren im Raum aus.
* ⏳ **Progress Veil & Haptisches Feedback:** Langes Drücken (Hold) auf Buttons wird mit einem eleganten Schleier-Effekt visualisiert und durch haptisches Feedback (falls vom Gerät unterstützt) bestätigt.
* 📱 **Swipeable Pop-up:** Wenn du mehr Geräte hast, als auf die Karte passen (Maximal 4 Slots), wird automatisch ein "Overflow"-Button (`...`) erstellt. Ein Klick darauf öffnet einen wunderschönen, wischbaren Pop-up-Dialog mit den restlichen Geräten. *Tipp: Langes Drücken auf den `...`-Button schaltet alle "versteckten" aktiven Geräte aus!*
* 🌡️ **Integrierte Sensoren:** Zeigt Temperatur, Luftfeuchtigkeit und den Fenster-/Türstatus direkt neben dem Raumnamen an.
* 🪟 **Smarte Rollladen-Steuerung:** Erkennt Rollläden automatisch. Zeigt Animationen beim Hoch-/Runterfahren und den prozentualen Öffnungsgrad direkt im Button an.
* 🖱️ **Visueller Editor:** Vollständig in die native Home Assistant Benutzeroberfläche integriert. Du brauchst kein YAML-Wissen, um die Karte perfekt einzustellen (inkl. Drag & Drop für Buttons!).

---

## 🚀 Installation

### Option 1: HACS (Empfohlen)
*(Sobald du das Repository zu HACS hinzugefügt hast, kannst du diese Anleitung nutzen)*
1. Öffne **HACS** in Home Assistant.
2. Gehe zu **Frontend** -> **Benutzerdefinierte Repositories** (Custom repositories).
3. Füge die URL deines GitHub-Repositories hinzu und wähle die Kategorie `Lovelace`.
4. Klicke auf **Herunterladen** und lade die Seite neu.

### Option 2: Manuell
1. Lade die Datei `smarvy-area-card.js` herunter.
2. Lege sie in deinem Home Assistant Verzeichnis unter `config/www/` ab.
3. Gehe in Home Assistant zu **Einstellungen** -> **Dashboards** -> **Ressourcen** (oben rechts auf die drei Punkte klicken).
4. Füge eine neue Ressource hinzu:
   * **URL:** `/local/smarvy-area-card.js`
   * **Typ:** `JavaScript Modul`

---

## ⚙️ Konfiguration

Die Karte verfügt über einen **hervorragenden visuellen Editor** direkt in Home Assistant. Du kannst alle Farben, Sensoren und Geräte bequem zusammenklicken. 

Für alle, die lieber **YAML** nutzen, hier ein ausführliches Beispiel:

```yaml
type: custom:smarvy-area-card
name: Wohnzimmer
icon: mdi:sofa
nav_path: /lovelace/wohnzimmer
temp_entity: sensor.wohnzimmer_temperatur
humidity_entity: sensor.wohnzimmer_luftfeuchtigkeit
window_entity: binary_sensor.wohnzimmer_fenster
show_door_closed: true
dark_text: false
cover_invert: true
max_buttons: 4
color_on: "#fdd835"
color_cover: "#34c759"
buttons:
  - entity: light.deckenlampe
    icon: mdi:ceiling-light
  - entity: cover.fenster_links
  - entity: switch.steckdose_tv
  - entity: fan.deckenventilator
  - entity: light.leselampe  # Rutscht automatisch ins Pop-up, da max_buttons auf 4 steht

### 📝 Parameter-Übersicht

| Parameter | Typ | Beschreibung |
| :--- | :--- | :--- |
| `name` | String | Der Name des Raums (z. B. "Wohnzimmer"). |
| `icon` | String | Das Haupt-Icon der Karte (Standard: `mdi:home`). |
| `nav_path` | String | (Optional) Ein Pfad (z. B. `/lovelace/kueche`), der geöffnet wird, wenn man auf die leere Fläche der Karte klickt. |
| `temp_entity` | Entity ID | (Optional) Sensor für die Temperatur. |
| `humidity_entity`| Entity ID | (Optional) Sensor für die Luftfeuchtigkeit. |
| `window_entity` | Entity ID | (Optional) Kontakt-Sensor für Fenster/Tür. |
| `show_door_closed`| Boolean | Wenn `true`, wird "Zu" angezeigt. Wenn `false` (Standard), wird der Sensor nur angezeigt, wenn er offen ist. |
| `dark_text` | Boolean | Aktiviert das helle Design mit dunkler Schrift. Perfekt für sehr helle Dashboard-Hintergründe. |
| `cover_invert` | Boolean | `true` invertiert die Rollladen-Anzeige (z. B. 0% = Offen). |
| `max_buttons` | Number | Wie viele Slots auf der Karte sichtbar sein sollen (1 bis 4). Weitere landen im Pop-up. |
| `buttons` | List | Liste deiner Entitäten (Unterstützt: light, switch, fan, cover, input_boolean). |

### 🎨 Farben anpassen (Optional)
Du kannst das Farbschema über den visuellen Editor oder per YAML komplett an deine Wünsche anpassen. Unterstützte Parameter sind z. B. `color_on`, `color_cover`, `color_door_open`, `color_door_closed` (und jeweils mit dem Suffix `_dark` für das helle Theme).

---

## 🕹️ Bedienung & Gesten

Damit deine Mitbewohner oder Gäste die Karte optimal nutzen können, hier ein kleiner Guide zu den eingebauten Gesten:

* **Mini-Buttons (Geräte):**
    * **Kurzes Tippen:** Schaltet das Gerät ein/aus (Toggle) oder startet/stoppt den Rollladen.
    * **Langes Drücken (Hold):** Öffnet den Home Assistant "More Info" Dialog (z. B. für Farbeinstellungen oder Helligkeit). Der *Progress Veil* zeigt an, wann lange genug gedrückt wurde.
* **Master Button (Großes Icon links):**
    * **Langes Drücken (Hold):** Führt einen "Master Off" aus – schaltet alle aktiven Lichter, Schalter und Ventilatoren dieses Raums auf einmal ab.
* **Overflow Button (`...`):**
    * **Kurzes Tippen:** Öffnet das flüssige Vollbild-Pop-up mit allen weiteren Geräten. Das Pop-up lässt sich per Swipe nach unten schließen.
    * **Langes Drücken (Hold):** Führt einen "Quick Off" für alle versteckten Geräte aus (schaltet alle Geräte aus, die im Pop-up sind).
