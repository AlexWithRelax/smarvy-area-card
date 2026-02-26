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
