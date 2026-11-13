# Projektprotokoll: Still-Tracker & Wellen-Tracker

**Stand:** 11. November 2026
**Entwicklung:** Lumo (Proton) im Dialog mit der Nutzerin/dem Nutzer

---

## Übergeordnetes Ziel

Zwei eigenständige, lokale HTML-Anwendungen zur Alltagserfassung (ohne Server, ohne Cloud):

1. **Still-Tracker** — Aufzeichnung von Stillzeiten (Links/Rechts) in Messreihen
2. **Wellen-Tracker** — Aufzeichnung von Wellen und Pausen (z. B. Trink-/Pauseschema), inkl. Blasensprung-Markierungen und Notizen

Beide laufen als einzelne HTML-Datei im Browser, Daten liegen ausschließlich im localStorage des jeweiligen Browsers/Geräts. Der Still-Tracker ist über **GitHub Pages** als PWA-artige Verknüpfung auf dem Smartphone installiert (Startbildschirm-Shortcut); Updates durch Überschreiben der `index.html` im Repository.

---

## Aktueller Stand Still-Tracker (v20, 11.11.2026)

- **Messreihen:** Fortführung über Browser-Neustarts hinweg; nur „Messreihe beenden" schließt eine Reihe. Jede gespeicherte Reihe wird über „Öffnen" sofort zur aktiven Reihe (egal ob vorher beendet) und ist sofort weitermessbar. „Neue Messreihe starten", Löschen einzelner Reihen in der Historie (mit Bestätigung).
- **Stillzeiten:** Start/Beenden über Hauptbutton, Seitenwahl Links/Rechts, Seitenwechsel mitten im Stillen splittet den Eintrag automatisch. Einstellung „Nach dem Stillen die Seite …" (automatisch wechseln / nicht ändern).
- **Notizen (v19/v20):** Pro Eintrag; erfassbar per Antippen der „Zuletzt"-Box, per Antippen des **laufenden Timers** (Notiz zur laufenden Stillzeit) und nachträglich per „Notiz"-Button in der Stillzeiten-Liste. Anzeige in Box, Liste, Zeitstrahl-Detail; Bestandteil des Backups.
- **Zeitstrahl:** Zeiträume 1 Std–7 Tage, Zoom ±, Blättern ◀/vor — Blättern stoppt exakt am Datenanfang (v19) bzw. an der Gegenwart. Balken antippbar für Details. Zoom-/Blickzustand wird **pro Messreihe** gespeichert und beim Öffnen wiederhergestellt.
- **Statistik:** Links/Rechts/Gesamt für heute.
- **Speichern (v18):** Sofortspeichern bei jeder Änderung (kein Debounce) plus Notfallspeichern bei `pagehide`, `beforeunload`, `visibilitychange`. Deutliche rote Warnung, falls localStorage verweigert (Privatmodus/Speicher voll).
- **Sicherung:** JSON-Export/Import (überschreibt beim Import alle Daten).
- **Speicherschlüssel:** `still-tracker-data-v3` (mit Legacy-Migration von v1/v2). Kompatibilität v18→v20 geprüft, Datenübernahme funktioniert.
- **Anleitung & Hilfe:** Eingebauter Dialog; Texte an das aktuelle Verhalten angepasst.

## Aktueller Stand Wellen-Tracker (v7.3, 10.11.2026)

- Wellen/Pausen über Hauptbutton; nach „Messung beenden" reaktivierbar (Zwischenzeit bleibt als Lücke im Zeitstrahl).
- Zeitachse umschaltbar: „Seit Start" (Dauer) / „Uhrzeit" (echte Uhrzeit).
- Blasensprünge und Notizen im Zeitstrahl; Trefferzonen aufgeteilt: Blasensprung nur obere, Notiz nur untere Hälfte (Grenze 75 px).
- Anleitung & Hilfe eingebaut; Autor-Signatur im Code (Kommentarblock, `AUTHOR_TAG`, Console).
- Messreihen: Öffnen macht die angezeigte zur aktiven (Wechsel erst bei „Welle starten" mit Bestätigung); Löschen alter Messreihen (v7.3).
- Kompatibilitäts-Fix v7.2: keine modernen JS-Funktionen (`findLast`, `.at()`, `roundRect` usw.), eingebauter Fehler-Wächter mit sichtbarer roter Meldung.

---

## Offene Punkte / mögliche nächste Schritte

- Sperrbildschirm-Steuerung (Wellen start/stop) ist mit Web-Technik **nicht möglich**; ggf. Medien-Benachrichtigung als Behelf diskutiert, aber verworfen.
- Größere Eintragsliste im Still-Tracker (aktuell max. 100) erwägen.
- Automatisierte Backups / Export-Erinnerungen für den Still-Tracker erwägen.
- Geräteübergreifende Datensynchronisation: nur via Export/Import möglich (lokale App ohne Server).

## Technische Vereinbarungen

- Bei jeder Änderung wird immer die **komplette neue Version** ausgeliefert (Code und/oder HTML-Datei), keine Snippets-only.
- Speicherschlüssel möglichst stabil halten, damit Daten über Versionswechsel erhalten bleiben.
-Versionshistorie im Kopf-Kommentar der Datei (Version, Datum, Änderungen).
