# ⛷️ FIS Ski Alpin World Cup - Live Wallpaper Engine

Dieses Projekt ist eine vollautomatisierte Lösung, um den **FIS Ski Alpin Nationencup** zu tracken und den aktuellen Saisonverlauf als **dynamisches Windows-Hintergrundbild** darzustellen.

Es besteht aus einem robusten Web-Scraper, der Live-Daten der FIS-Webseite extrahiert, und einem Visualisierungs-Modul, das diese Daten in ästhetische Graphen verwandelt und direkt in das Desktop-Wallpaper integriert.

![Preview Graph](https://github.com/user-attachments/assets/43904063-02b8-4a69-8303-69011e862a80)

## ✨ Features

*   **Advanced Web Scraping (Selenium):** Umgeht Probleme mit dynamisch geladenem JavaScript-Content auf der FIS-Webseite, an denen herkömmliche Bibliotheken (wie `requests`) scheitern.
*   **Intelligente Datenbereinigung:** Filtert fehlerhafte Datenpunkte (z.B. FIS-Codes oder Laufzeiten, die fälschlicherweise als Punkte interpretiert werden) durch eine strikte Weltcup-Punkte-Logik (`<= 100`).
*   **Daten-Visualisierung (Matplotlib & Pandas):** Erstellt professionelle Liniendiagramme des Saisonverlaufs (Kumulierte Punkte).
    *   *Smart Labels:* Verhindert das Überlappen von Beschriftungen, wenn Nationen punktgleich sind.
    *   *Custom Styling:* Offizielle Landesfarben für Top-Nationen, Transparenz für kleinere Nationen.
    *   *Chronologische Achse:* Korrekte Darstellung der Rennen unabhängig von nicht-sequenziellen Race-IDs.
*   **Live Wallpaper Integration:** Manipuliert das Windows-Hintergrundbild (`ctypes`), um das Diagramm nahtlos in ein bestehendes Wallpaper einzubetten.

## 📂 Projektstruktur

Das Projekt besteht aus vier Hauptkomponenten:

### 1. `scraper.py` (Data Extraction)
Das Herzstück der Datenbeschaffung.
*   Nutzt **Selenium WebDriver**, um die resultatsbasierten DOM-Elemente der FIS-Seite zu laden.
*   Iteriert durch eine Liste von Race-IDs der aktuellen Saison.
*   Extrahiert Platzierungen und Punkte pro Nation.
*   Exportiert bereinigte Daten in eine strukturierte JSON-Datei.

### 2. `visualizer.py` (Data Processing & UI)
Verarbeitet die Rohdaten und aktualisiert den Desktop.
*   Lädt die `results.json`.
*   Berechnet mit **Pandas** die kumulierten Summen (Running Total) pro Nation.
*   Erstellt den Graphen mit **Matplotlib** (inkl. "Smart Labeling" Logik für USA/NOR Konflikte).
*   Nutzt **Pillow (PIL)**, um den Graphen auf ein Basis-Bild zu kleben.
*   Setzt das neue Bild als Windows-Wallpaper.

### 3. `results.json` (Database)
Speichert den aktuellen Stand der Saison in einem maschinenlesbaren Format.
*   Struktur: Liste von Events mit zugehöriger Race-ID und den erreichten Punkten pro Nation an diesem Tag.

### 4. `automate.bat` (Automation)
Ein einfaches Batch-Skript, um den Prozess im Hintergrund zu starten (z.B. via Windows Task Scheduler oder Autostart), damit das Wallpaper immer aktuell bleibt, ohne manuelles Eingreifen.

## 🛠️ Technologien & Requirements

*   **Python 3.10+**
*   **Selenium** (Browser Automation)
*   **Pandas** (Dataframes & Berechnung)
*   **Matplotlib** (Plotting)
*   **Pillow** (Image Manipulation)
*   **Chrome WebDriver**

## 🚀 Installation & Nutzung

1.  **Repository klonen:**
    ```bash
    git clone https://github.com/DEIN_USER/projekt_ski.git
    ```

2.  **Abhängigkeiten installieren:**
    ```bash
    pip install pandas matplotlib selenium pillow webdriver-manager
    ```

3.  **Konfiguration:**
    *   Pfade in den Python-Skripten anpassen (`BASE_IMAGE_PATH` für dein Wallpaper).
    *   Ggf. Race-IDs im Scraper für die neue Saison aktualisieren.

4.  **Starten:**
    *   Scraping starten: `python scraper.py`
    *   Visualisierung starten: `python visualizer.py`
    *   Oder alles zusammen über `automate.bat`.

---
*Created with ❤️ for Ski Alpin Fans.*
