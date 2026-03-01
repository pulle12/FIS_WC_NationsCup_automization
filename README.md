# ⛷️ FIS Ski Alpin Nationen-Cup 2025/26 – Wallpaper Engine

Dieses Projekt aktualisiert automatisch deinen Windows-Hintergrund mit dem aktuellen Stand des **FIS Ski Alpin Nationen-Cups**.

[https://github.com/user-attachments/assets/33169732-ac67-403a-93e7-c59432491966]

Es besteht aus:
- einem Scraper für die FIS-Ergebnisse,
- einer Auswertung mit kumulierten Punkten pro Nation,
- und einer Visualisierung, die direkt ins Wallpaper eingebettet wird.

## Funktionen

- **Web-Scraping mit Selenium:** Liest Ergebnisdaten von der FIS-Seite, auch bei dynamisch geladenen Inhalten.
- **Punkte-Filterung:** Berücksichtigt nur gültige Weltcup-Punkte (max. `100` pro Athlet/Ergebniszeile).
- **Saisonverlauf als Diagramm:** Erstellt mit `pandas` + `matplotlib` einen laufenden Nationen-Cup-Graphen.
- **Wallpaper-Update unter Windows:** Setzt das erzeugte Bild per `ctypes` als Desktop-Hintergrund.

## Projektstruktur

- `scraper.py`
    - Holt Ergebnisse über Race-IDs von der FIS-Seite.
    - Speichert bereinigte Punkte in `results.json`.

- `ski_nationencup_25-26.py`
    - Liest `results.json` ein.
    - Berechnet kumulierte Punkte je Nation.
    - Rendert das Diagramm und kombiniert es mit dem Basisbild aus `pics`.
    - Setzt das Ergebnis als Windows-Wallpaper.

- `results.json`
    - Datenspeicher mit Rennen (`race_id`) und Punkten pro Nation.

- `automate.bat`
    - Führt nacheinander `scraper.py` und `ski_nationencup_25-26.py` aus.

## Voraussetzungen

- Python `3.10+`
- Google Chrome (installiert)
- Pakete:
    - `selenium`
    - `webdriver-manager`
    - `beautifulsoup4`
    - `pandas`
    - `matplotlib`
    - `pillow`

## Einrichtung

1. Abhängigkeiten installieren:

     ```bash
     pip install selenium webdriver-manager beautifulsoup4 pandas matplotlib pillow
     ```

2. Optional anpassen:
     - In `ski_nationencup_25-26.py` den Pfad `BASE_IMAGE_PATH` auf dein gewünschtes Hintergrundbild setzen.
     - In `scraper.py` die `season_races` bei Bedarf aktualisieren.

## Nutzung

- Einzeln starten:

    ```bash
    python scraper.py
    python ski_nationencup_25-26.py
    ```

- Oder automatisch über:

    ```bash
    automate.bat
    ```

---
Für Fans des alpinen Ski-Weltcups gebaut.
