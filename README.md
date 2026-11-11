# MyTasks

**MyTasks** ist die Aufgabenverwaltung im MyDigital-System. Die App läuft als Web-App und kann auf unterstützten Geräten installiert werden.

## Funktionen

- Aufgaben mit Titel, Beschreibung, Fälligkeitsdatum und Priorität erstellen
- Aufgaben bearbeiten, abhaken und löschen
- Automatische Sortierung: offene Aufgaben zuerst, danach nach Fälligkeitsdatum
- Überfällige Aufgaben erkennen
- Suche und Filter für offene und erledigte Aufgaben
- Persönliche Akzentfarbe
- Gemeinsame Anmeldung über das MyDigital-Konto
- Synchronisierung über Supabase mit MyKalender
- PWA-Grundfunktionen für Installation und Offline-Aufruf der App-Oberfläche

## Zusammenspiel mit MyKalender

MyTasks und MyKalender verwenden dasselbe Supabase-Projekt und dieselbe Anmeldung. Aufgaben liegen in der Tabelle `public.tasks`:

- `id`: eindeutige Aufgaben-ID
- `owner`: Konto-ID des Besitzers
- `data`: Aufgabeninhalt als JSON
- `created_at`: Erstellungszeitpunkt

Die Tabelle hat Row Level Security (RLS). Nutzer können nur ihre eigenen Aufgaben lesen und ändern. MyKalender zeigt die Aufgaben im Menüpunkt **Aufgaben** an und kann den Erledigt-Status speichern.

**Live-Synchronisierung:** Änderungen an Aufgaben werden über Supabase Realtime zwischen MyTasks und MyKalender übertragen. Falls die Verbindung vorübergehend ausfällt, kannst du die Ansicht über „Aktualisieren“ neu laden.

## Technik

- HTML, CSS und JavaScript
- Supabase Auth und PostgreSQL
- GitHub Pages
- Progressive Web App (Manifest und Service Worker)

## Datenschutz und lokale Daten

Die App verwendet den öffentlichen Supabase Publishable Key im Browser. Dieser Schlüssel ist kein Admin-Schlüssel; der Datenzugriff wird durch Supabase-RLS-Regeln begrenzt. Passwörter werden nicht in der App gespeichert.

Lokale Aufgaben werden beim ersten erfolgreichen Anmelden mit dem Konto synchronisiert. Nach dem Abmelden werden die Aufgaben aus der lokalen Ansicht entfernt, damit sie nicht versehentlich im nächsten Konto angezeigt werden.

## Veröffentlichung

- Repository: `kotzschfelix-sudo/MyTasks`
- Website: https://kotzschfelix-sudo.github.io/MyTasks/
- Dashboard: https://kotzschfelix-sudo.github.io/MyDigital/
