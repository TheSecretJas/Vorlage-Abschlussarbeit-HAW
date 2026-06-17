
# Changelog
Alle wesentlichen Änderungen an dieser LaTeX-Vorlage werden in dieser Datei dokumentiert.

## [5.3.0] - 2026-06-17

### Changed
- **Setup:** Nutzerbefehle für das Dokument werden jetzt in Settings innitialisiert und dann in Setup neu definiert. Ermöglicht das Entfernen des Symbolverzeichnisses
- **Layout:** 
  - **Absatzabstand:** Globale Definition von `\parskip` auf 18pt (mit einer Toleranz von `plus 2pt minus 1pt`) am Dokumentenanfang hinzugefügt. Dies dynamische Abstände zwischen Absätzen, ohne manuelle Umbrüche erzwingen zu müssen.
  - **Überschriften:** Die vertikalen Abstände vor und nach Titeln (`\section`, `\subsection`, `\subsubsection`) wurden mithilfe des Pakets `titlespacing`  geändert, um ein an den Absatzabstand angelehntes Schriftbild zu erzeugen.
  - **Listen und Aufzählungen:** Integration des Pakets `enumitem`. Störende Abstände vor und nach Listen (`topsep`, `partopsep`) wurden auf 0pt gesetzt, der Abstand zwischen Listenpunkten (`itemsep`) auf feste 6pt fixiert.


---

## [5.2.0] - 2026-05-26

### Fixed
- **Seitenlayout (Abstract):** Bug behoben, der den verfügbaren Schreibplatz auf der Abstract-Seite drastisch reduziert hat. Das Layout wird nun lokal für diese Seite angepasst und anschließend mit `\restoregeometry` wieder auf den Standard zurückgesetzt.

---

## [5.1.0] - 2026-05-23

### Changed
- **Titelseite:** Anpassung des Titelblatts an die neueste, offizielle Vorlage der Fakultät. Aufgrund der fehlenden Detaillstruktur seitens der HAW, ist aktuell noch keine 100%ige Übereinstimmung möglich.

### Fixed
- **Rechtschreibung:** Fehler im Code des Symbolverzeichnisses behoben ("Matrizen" statt "Matritzen").

---

## [4.7.0] - 2026-04-27

### Added
- **Sortierlogik (DIN):** Vollständige Neudefinition der Symbol-Benennung und der Xindy-Sortierlogik des Symbolverzeichnisses. Implementierung einer Ersetzungslogik via `\ExplSyntaxOn`, bei der griechische Makros systematisch mit numerischen Präfixen versehen werden (z. B. `\alpha` zu `01alpha`). Dies erzwingt eine saubere, normgerechte Sortierung.

### Fixed
- **Namenskollisionen:** Fehler behoben, bei dem die redundante Benennung von Variablen zum Absturz führte. Namensgleichheiten werden nun durch eine erweiterte Suffix-Logik robust abgefangen und entsprechend sortiert.

---

## [4.6.0] - 2025-12-12

### Changed
- **Schriftarten:** Komplette Neudefinition der globalen Fonts zur Behebnung von Inkonsistenzen. Setup basiert nun auf `textcomp`, `lmodern` und skaliertem `helvet` als serifenloser Standardschrift (`\sfdefault`). `mathastext` sorgt für die korrekte, aufrechte Darstellung im Mathemodus
- **Kopfzeile:** Logik der Header-Darstellung umgeschrieben. Nutzt nun ein neudefiniertes `firstleftmark` für ein saubereres Auslesen der Kapitelnamen. Behebt zudem ein Problem, bei dem die `leftmark` auf ungraden Seiten eingerückt war. Funktioniert aktuell nur bis inklusive Texlive V2024

---

## [4.5.0] - 2025-11-12

### Added
- **Fallback-Commands:** Sämtliche user-definierten Befehle werden nun via `\providecommand` mit leerem Inhalt versteckt initialisiert. Dies verhindert fatale Kompilierungsfehler, falls Endnutzer diese Befehle versehentlich aus dem Hauptdokument löschen.

---

## [4.0.0] - 2025-10-14

### Added
- **Code-Listings:** Das `listings`-Paket wurde integriert, inklusive umfassender Definitionen für Syntax-Highlighting (Text, Keywords, Strings).

### Changed
- **Referenzierung:** Codeausschnitte in die `\autoref`-Logik eingebunden.
- **Usability:** Diverse bestehende Makros wurden umgeschrieben und vereinfacht, um die Anwendung für LaTeX-Anfänger intuitiver zu gestalten.

---

## [3.6.0] - 2025-09-26

### Fixed
- **Symbolverzeichnis:** Kritischen Bug behoben, bei dem die Nutzung von griechischen Buchstaben als Indizes den Compiler zum Absturz brachte.

---

## [3.5.0] - 2025-09-09

### Changed
- **Struktur:** Vollständige Neustrukturierung und Umbenennung der Template-Kapitel, um den realen Aufbau einer Bachelorarbeit exakter abzubilden.
- **Beispiele:** Alle Code- und Textbeispiele innerhalb der Vorlage tiefgreifend überarbeitet.

---

## [3.4.0] - 2025-06-22

### Added
- **Sperrvermerk:** Template für einen offiziellen Sperrvermerk (NDA) für Abschlussarbeiten in Kooperation mit Unternehmen implementiert.

### Changed
- **Typografie:** Anpassung der globalen Schriftart und Schriftgröße zur signifikanten Verbesserung der Lesbarkeit

---

## [3.3.0] - 2025-01-20

### Added
- **Danksagung:** Vorlagenseite für eine Danksagung (Acknowledgments) hinzugefügt.

### Changed
- **Erklärung:** Die Selbstständigkeitserklärung wurde inhaltlich und optisch überarbeitet.

---

## [3.2.0] - 2025-01-19

### Added
- **Inline-Dokumentation:** Umfangreiche Kommentare direkt im Quellcode hinzugefügt, um die Funktionalität der Makros für Endnutzer verständlicher zu machen.

### Changed
- **Tabellen:** Logik für komplexe Tabellen erneut überarbeitet, um das Verhalten bei Seitenumbrüchen stabiler zu machen.

---

## [3.1.0] - 2025-01-12

### Changed
- **Tabellen-Umgebung:** Neudefinition der `ltablex`-Nutzung. Tabellen dieser Art funktionieren eigenständig und benötigen keine umschließende `figure`-Umgebung mehr
- **Seitenlayout:** Überarbeitung der doppelseitigen Struktur (`twoside`). Option hinzugefügt, um die Positionierung der ersten Seiten flexibel zu verschieben
- **Dokumentation:** Bedienhinweise und Beispiele im Template aktualisiert.

---

## [3.0.0] - 2025-01-03

### Added
- **Anhangs-Verzeichnis:** Entwicklung der `appendixtoc`-Logik und vollständige Integration in die Anhangsstruktur zur sauberen Trennung vom Hauptverzeichnis.
- **Beispiele:** Neue Praxisbeispiele in die Datei `Stand der Technik.tex` eingefügt.

### Changed
- **Literatur & Einheiten:** Das Literaturverzeichnis-Setup und die Einheitenmakros wurden grundlegend überarbeitet und stabilisiert.

---

## [2.8.0] - 2024-10-13

### Added
- **PDF-Metadaten:** Einbindung von Metadaten in die generierte PDF 
- **Abstract & Dokumentenstart:** Erstellung der Abstract-Seiten und des grundlegenden Dokumentenbeginns 
- **Nummerierung:** Wissenschaftliche Seitennummerierung implementiert (römische Ziffern im Vorspann, danach arabisch) 
- **Literatur:** Standardliteratur als Basis hinzugefügt 
- **Erklärungen:** Vorlage für die Selbstständigkeitserklärung erstellt 
- **Dokumentation:** Bedienungsanleitung zur Nutzung der Vorlage hinzugefügt.

### Changed
- **Abbildungen:** Komplettes Rework der Figure-Captions, inklusive kapitelweiser Darstellung und Anpassung auf eine kleinere Schriftart 
- **Titelseite:** Komplette Neuüberarbeitung des Titelblatts nach den Vorgaben der offiziellen HAW-Vorlage.

### Fixed
- **Symbolverzeichnis:** Diverse Bugfixes bei der Darstellung behoben 
- Allgemeine Bugfixes und Stabilitätsverbesserungen im Zeitraum bis Ende Juni 2024.

---

## [2.5.0] - 2024-04-26

### Added
- **Overleaf-Release:** Erste lauffähige Version auf Overleaf veröffentlicht.
- **Verzeichnisse:** 
  - Automatisiertes Symbolverzeichnis mit `xindy`, `environ` und `tabularx` 
  - Programmierung des Abkürzungsverzeichnisses (28.03.2024).
- **Custom Commands:**
  - Eigene Befehle zum effizienten Einbinden von Bildern (`\newfigure`), SVGs (`\newsvg`) und Multi-Figures (`\newmultifig`) inkl. automatisierter FloatBarriers.
  - Quality-of-Life Makros für römische Zahlen (`\uproman`, `\lowroman`) und eingekreiste Zahlen (`\circlearound`).
- **Einheiten:** Einheitenmakros für eine konsistente Darstellung eingeführt 
- **Titelseite:** Erste Version des Titelblatts erstellt 

### Changed
- **Referenzierung:** Standard-Referenzen (`autoref`) umdefiniert ("section" wird zu "Kapitel", Equations zu "Gleichung (x)").
- **Symbolverzeichnis:** Grundlegendes Rework der Struktur
- **Dateistruktur:** Komplette Umstrukturierung aller TeX-Dateien für eine bessere Übersichtlichkeit und Modularität
- **Layout-Setup:** Basis-Packages (Babel, biblatex, geometry, fancyhdr) und grundlegende Layouteinstellungen konfiguriert 

### Fixed
- Fortlaufende kleine Bugfixes und Anpassungen der Standardeingaben während der initialen Entwicklungsphase 

---

## [2.0.0] - 2024-03-28

### Added
- **Abkürzungsverzeichnis:** Programmierung und Integration eines eigenständigen Abkürzungsverzeichnisses
- **Einheitenmakros:** Einführung globaler Einheiten-Kürzel im Mathemodus zur Gewährleistung einer konsistenten, aufrechten Darstellung physikalischer Einheiten 
- **Titelseite:** Erste funktionale Rohversion der Titelseite implementiert 

### Changed
- **Symbolverzeichnis:** Grundlegendes Rework des Symbolverzeichnisses zur Optimierung der Spaltenbreiten bei längeren Einheiten- oder Textbeschreibungen

---

## [1.1.0] - 2023-11-10

### Added
- **Symbolverzeichnis:** Dynamisches und automatisiertes Symbolverzeichnis unter Verwendung der Packages `xindy`, `environ` und `tabularx` aufgesetzt.
- **Verweis-Optimierung:** Umdefinition der Standard-`autoref`-Ausgaben für den deutschen Sprachraum.

---

## [1.0.0] - 2023-08-15

### Added
- **Custom Figure Commands:** Programmierung der Makros `\newfigure`, `\newsvg` und `\newmultifig`.
- **Design-Makros:** Eigene mathematische Hilfsbefehle wie `\uproman`/`\lowroman` und `\circlearound`.
- **Seitenlayout:** Definition des Satzspiegels über das `geometry`-Paket.
- **Kopf-/Fußzeilen:** Einrichtung von `fancyhdr` mit angepassten Schriftgrößen-Makros.

---

## [0.1.0] - 2023-06-13

### Added
- **Initialer Commit:** Erstellung des initialen Projekt-Setups inklusive der grundlegenden Packages, basierend auf Laborberichten
