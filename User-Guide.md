# User Guide – LaTeX-Vorlage Abschlussarbeit HAW

Diese Anleitung dokumentiert den Aufbau der Vorlage, die Ersteinrichtung, sämtliche
Spezialbefehle sowie die wichtigsten Anpassungs- und Best-Practice-Hinweise.

> Stand: Vorlagen-Version 5.4.0 · Repository: <https://github.com/TheSecretJas/Vorlage-Abschlussarbeit-HAW>

---

## 1. Grundlegender Aufbau – Orientierung im Projekt

Die Vorlage ist modular aufgebaut. Die Datei `main.tex` bindet alle
Bausteine per `\input` ein und bestimmt ausschließlich deren Reihenfolge. Inhalt,
Layout und Nutzereingaben sind sauber voneinander getrennt.

```
Vorlage-Abschlussarbeit-HAW/
├── main.tex                      # Hauptdatei: Kapitelreihenfolge, PDF-Metadaten, Titelseitenwahl
├── Literatur.bib                 # BibTeX-Datenbank für saemtliche Quellen
├── CHANGELOG.md                  # Änderungshistorie der Vorlage
├── User-Guide.md                 # Diese Anleitung
│
├── Bilder/                       # Ablageort fuer alle Grafiken (graphicspath)
│
├── Kapitel/                      # Der eigentliche Fließtext
│   ├── 00-Symbole.tex            # Zentrale Eingabe aller Symbole und Abkürzungen
│   ├── 01-Einleitung.tex
│   ├── 02-Theoretische Grundlagen.tex
│   ├── 03-Methodik.tex
│   ├── 04-Ergebnisse und Diskussion.tex
│   ├── 05-Ausblick.tex
│   └── 100-Anhang.tex
│
└── misc/                         # Konfiguration und Sonderseiten
    ├── Setup.tex                 # >> Hier sämtliche persönlichen Daten eintragen <<
    ├── Einheitenmacros.tex       # Einheiten-Kürzel für den Mathemodus
    ├── Sperrvermerk.tex          # Optionaler Sperrvermerk (NDA)
    ├── Danksagung.tex            # Optionale Danksagung
    └── Background/               # Technischer Unterbau (im Regelfall nicht anzupassen)
        ├── Settings.tex          # Pakete, globales Layout, Custom Commands
        ├── Symbolverzeichnis.tex # Logik fuer Symbol- und Abkürzungsverzeichnis
        ├── Dokumentbeginn.tex    # Ablauf des Vorspanns (Abstract, Verzeichnisse)
        ├── titlepage.tex         # Alternative, schlichte Titelseite
        ├── Logos/                # HAW-Logos (HAW_Marke etc.)
        └── HAW_Stil/
            ├── Titelpage_haw_stil.tex        # Offizielles HAW-Titelblatt
            ├── Abstractpage.tex              # Kurzreferat / Abstract (DE + EN)
            └── Selbstständigkeitserklärung.tex
```

Die für die tägliche Arbeit relevanten Dateien im Überblick:

| Anliegen | Zuständige Datei |
|---|---|
| Persönliche Daten, Titel, Prüfer, Abstract eintragen | `misc/Setup.tex` |
| Text verfassen | `Kapitel/01-...` bis `Kapitel/05-...` |
| Symbole und Abkürzungen eintragen | `Kapitel/00-Symbole.tex` |
| Quellen verwalten | `Literatur.bib` |
| Reihenfolge sowie Ein- und Ausblenden von Seiten steuern | `main.tex`, `misc/Background/Dokumentbeginn.tex` |
| Ränder, Schrift und Abstände anpassen | `misc/Background/Settings.tex` |
| Eigene Einheiten ergänzen | `misc/Einheitenmacros.tex` |

Als Grundregel gilt: Sämtliche Dateien unterhalb von `misc/Background/` bilden den
technischen Kern der Vorlage und müssen für eine gewöhnliche Arbeit nicht angepasst
werden.

---

## 2. Ersteinrichtung

### 2.1 Umgebung und Compiler

Zum Kompilieren wird folgende Werkzeugkette benötigt:

- **pdfLaTeX** als Compiler
- **Biber** für die Literaturverwaltung (`biblatex`, Zitierstil `ieee`)
- **makeglossaries mit xindy** für Symbol- und Abkürzungsverzeichnis (Sortierung
  `german-din`)
- **Shell-Escape und Inkscape**, sofern SVG-Grafiken über `\newsvg` eingebunden
  werden

Auf **Overleaf** ist die Vorlage unmittelbar lauffähig: Den Compiler auf
*pdfLaTeX* stellen; unter *Menu → Settings* ist Biber bereits als Standard
hinterlegt. Xindy und Inkscape stehen serverseitig zur Verfügung.

> **Hinweis:** Die Logik der Kopfzeile (`firstleftmark`) arbeitet gegenwärtig
> zuverlässig bis einschließlich **TeXLive 2024**. Bei neueren lokalen
> Distributionen kann die Darstellung des Kapitelnamens in der Kopfzeile
> abweichen.

### 2.2 Persönliche Daten eintragen (`misc/Setup.tex`)

Der gesamte personalisierte Inhalt wird an **einer** zentralen Stelle gepflegt.
Alle Felder werden über `\renewcommand` gesetzt und automatisch an Titelseite,
Abstract, Sperrvermerk, Selbstständigkeitserklärung sowie an die PDF-Metadaten
verteilt.

```latex
\renewcommand{\Autor}{Vorname Nachname}
\renewcommand{\Vorname}{Vorname}
\renewcommand{\Nachname}{Nachname}
\renewcommand{\Matrikelnummer}{1234567}
\renewcommand{\Datum}{01.08.2026}

\renewcommand{\Titel}{Dein spannendes Thema}
\renewcommand{\TitelEN}{Your Exciting Title}

\renewcommand{\Dokumentenart}{Bachelorarbeit}   % oder Masterarbeit, Studienarbeit ...
\renewcommand{\Pruefungsart}{Bachelorpruefung}

\renewcommand{\Erstpruefer}{Erstpruefer: Prof. Dr.-Ing. ...}
\renewcommand{\Zweitpruefer}{Zweitpruefer: Prof. Dr.-Ing. ...}
\renewcommand{\Betreuer}{Industrieller Betreuer: Name}
\renewcommand{\Firmenname}{Firma XY AG}
\renewcommand{\Firma}{in Zusammenarbeit mit:\\ \Firmenname\\ Abteilung XX\\ Strasse Nr.\\ PLZ Ort}

\renewcommand{\Stichworte}{Stichwort 1, Stichwort 2}
\renewcommand{\StichworteEN}{Keyword 1, Keyword 2}
\renewcommand{\Zusammenfassung}{Deutsche Kurzzusammenfassung ...}
\renewcommand{\ZusammenfassungEN}{English abstract ...}
```

**Wichtig:** Diese Befehle werden in `Settings.tex` bereits leer per
`\providecommand` initialisiert. Wird also versehentlich eine Zeile in `Setup.tex`
gelöscht, bricht die Kompilierung nicht ab – das betreffende Feld bleibt lediglich
leer.

### 2.3 KI-Verwendungshinweis

Am Ende von `Setup.tex` ist der optionale KI-Hinweis als `\defbibnote` hinterlegt:

```latex
\defbibnote{ai_disclosure}{%
  \small\itshape Hinweis zur Verwendung von KI-Werkzeugen: ...}
```

- **Text anpassen:** direkt in `Setup.tex`.
- **Ein- und Ausblenden:** in `main.tex` beim Literaturverzeichnis. Der Hinweis
  erscheint als Vorbemerkung oberhalb des Verzeichnisses:

```latex
% mit Hinweis:
\printbibliography[prenote={ai_disclosure},heading=bibintoc, title={Literaturverzeichnis}]
% ohne Hinweis: das prenote-Argument entfernen
\printbibliography[heading=bibintoc, title={Literaturverzeichnis}]
```

### 2.4 Verwendete Seiten festlegen (Sonderseiten steuern)

Der Vorspann wird in `misc/Background/Dokumentbeginn.tex` zusammengesetzt. Dort
wird bestimmt, welche optionalen Seiten erscheinen:

| Seite | Datei | Ein- und Ausschalten |
|---|---|---|
| Sperrvermerk (NDA) | `misc/Sperrvermerk.tex` | `\input{misc/Sperrvermerk}` in `Dokumentbeginn.tex` auskommentieren |
| Danksagung | `misc/Danksagung.tex` | `\input{misc/Danksagung}` auskommentieren |
| Symbolverzeichnis | – | in `Dokumentbeginn.tex` die Zeile `\printglossary[type=symbols,...]` auskommentieren |
| Abkürzungsverzeichnis | – | Zeile `\printglossary[type=acronym,...]` auskommentieren |

Wird eine Sonderseite nicht benötigt, sollte der zugehörige `\input`
auskommentiert statt die Datei gelöscht werden – so bleibt sie für eine spätere
Verwendung erhalten.

### 2.5 Titelseite auswählen (`main.tex`)

Es stehen zwei Titelseiten zur Verfügung. Standard ist das offizielle HAW-Layout:

```latex
% Offizielles HAW-Titelblatt (Standard):
\input{misc/Background/HAW_Stil/Titelpage_haw_stil}

% Alternative, schlichte Version:
%\input{misc/Background/titlepage}
```

Zum Umschalten wird die jeweils andere Zeile auskommentiert.

### 2.6 Doppelseitiges Layout (`twoside`)

Die Vorlage ist auf `twoside` eingestellt, damit Kapitel in einem gedruckten,
gebundenen Dokument auf der korrekten Seite beginnen. Um eine erste Inhaltsseite
gezielt nach rechts zu verschieben, sind an mehreren Stellen vorbereitete
Leerseiten hinterlegt:

```latex
\null\thispagestyle{empty}
\clearpage
```

Diese Blöcke werden bei Bedarf ein- oder auskommentiert, bis der Seitenumbruch
passt.

---

## 3. Spezielle Funktionen und Makros

### 3.1 Bilder und Grafiken

Sämtliche Grafiken gehören in den Ordner `Bilder/` (bereits als `graphicspath`
gesetzt). Die folgenden Makros erzeugen automatisch ein `\label` der Form
`fig:<Dateiname>` und setzen im Anschluss eine `\FloatBarrier`.

| Befehl | Zweck |
|---|---|
| `\newfigure[Kurztitel]{Breite}{Datei}{Bildunterschrift}` | Einzelbild (PNG/JPG/PDF) |
| `\newsvg[Kurztitel]{Breite}{Datei}{Bildunterschrift}` | Vektorgrafik im SVG-Format |
| `\newmultifig{Datei1}{Unterschrift1}{Datei2}{Unterschrift2}` | Zwei Bilder nebeneinander |

- **Breite** ist ein Faktor von `\textwidth` (z. B. `0.6` entspricht 60 %
  Textbreite).
- **Kurztitel** (optionales Argument in `[...]`) erscheint im
  Abbildungsverzeichnis; entfällt er, wird die vollständige Bildunterschrift
  verwendet.

```latex
\newfigure[Flughafen]{0.6}{flughafen.jpg}{Ein Bild vom Flughafen. Quelle: \cite{DIN_EN_2597}}
\FloatBarrier
In \autoref{fig:flughafen.jpg} ist der Flughafen zu sehen.
```

### 3.2 Referenzieren mit `\autoref`

`\autoref{label}` ergänzt automatisch das passende deutsche Wort:

| Element | Label-Konvention | Ausgabe |
|---|---|---|
| Kapitel/Abschnitt | `\label{chap:...}` | *Kapitel X* |
| Unterkapitel | (section-Label) | *Unterkapitel X* |
| Abbildung | `fig:...` (automatisch) | *Abbildung X* |
| Tabelle | `tab:...` | *Tabelle X* |
| Gleichung | `eq:...` | *Gleichung (X)* |

### 3.3 Einheiten (Mathemodus)

Definiert in `misc/Einheitenmacros.tex`. Jedes Makro setzt einen schmalen
Vorabstand und stellt die Einheit aufrecht dar. Verwendung **im Mathemodus**:
`$9{,}81\mpss$`.

| Makro | Einheit | Makro | Einheit |
|---|---|---|---|
| `\mm` `\cm` `\m` | mm, cm, m | `\N` `\kN` | N, kN |
| `\mps` `\mpss` | m/s, m/s² | `\Nm` `\Nmm` `\kNm` | Nm, Nmm, kNm |
| `\kmh` | km/h | `\Npmm` | N/mm² |
| `\g` `\kg` `\ton` | g, kg, t | `\Pa` `\MPa` `\GPa` | Pa, MPa, GPa |
| `\s` `\h` | s, h | `\dichte` | kg/m³ |
| `\Hz` `\kHz` | Hz, kHz | `\kinvis` | m²/s |
| `\K` `\C` | K, °C | `\dB` | dB |
| `\W` | W | `\mum` | µm |

Fehlt eine Einheit, wird sie nach demselben Muster in `Einheitenmacros.tex`
ergänzt:

```latex
\newcommand*{\kWh}{\ensuremath{\,\mathrm{kWh}}}
```

### 3.4 Weitere Quality-of-Life-Makros (`Settings.tex`)

| Befehl | Zweck |
|---|---|
| `\uproman{n}` / `\lowroman{n}` | römische Zahlen (groß / klein), z. B. `\uproman{4}` ergibt IV |
| `\circlearound{x}` | Zeichen einkreisen |
| `\plus` / `\minus` | verkleinertes Plus/Minus für Hochstellungen |
| `\newparagraph{Titel}` | benannter Absatz mit Label |
| `\changefont` / `\changefontbig` | Schriftgrößen der Kopfzeile |

### 3.5 Tabellen

Standard ist `tabularx` in Kombination mit `ltablex`. Solche Tabellen sind
seitenumbruchfähig und benötigen **keine** umschließende `figure`-Umgebung.
Spaltentypen: `X` (dehnbar), `l`/`c`/`r` (fest).

```latex
\begin{tabularx}{\columnwidth}{|X|X|}
\caption{Beispieltabelle}\label{tab:beispiel} \\ \hline
\textbf{Ueberschrift 1} & \textbf{Ueberschrift 2} \\ \hline
Wert 1 & Wert 2 \\ \hline
\end{tabularx}
```

Für mehrseitige Tabellen mit wiederholtem Kopf stehen `\endfirsthead`, `\endhead`,
`\endfoot` und `\endlastfoot` zur Verfügung (Beispiel in
`Kapitel/02-Theoretische Grundlagen.tex`).

### 3.6 Code-Listings

Umgesetzt über `listings` mit vordefiniertem `spyderstyle` (Zeilennummern,
Syntax-Highlighting). Die Bezeichnung im Verzeichnis lautet *Code-Ausschnitt*.

```latex
\begin{lstlisting}[language=python]
def hallo():
    print("Welt")
\end{lstlisting}
```

---

## 4. Symbolverzeichnis und Abkürzungen

Alle Symbole und Abkürzungen werden **zentral** in `Kapitel/00-Symbole.tex`
eingetragen. Die Verzeichnisse (Nomenklatur, Abkürzungen) entstehen daraus
automatisch und werden normgerecht nach DIN sortiert – auch griechische Buchstaben
werden an der korrekten Stelle einsortiert.

### 4.1 Symbole eintragen

Es existieren drei Kategorien mit jeweils einem Befehl:

```latex
% Formelzeichen (Skalare und Vektoren):
% \newformulasymbol{<Bedeutung>}{<Zeichen>}{<Einheit>}
\newformulasymbol{Beschleunigung}{a}{m/s^2}
\newformulasymbol{Wellenlaenge}{\lambda}{m}

% Matrizen (Zeichen wird automatisch fett gesetzt):
% \newmatrix{<Bedeutung>}{<Zeichen>}{<Einheit>}
\newmatrix{Massen}{M}{kg}

% Indizierungen:
% \newindice{<Bedeutung>}{<Zeichen>}
\newindice{experimentell ermittelt}{ex}
```

- Das **Zeichen** wird automatisch im Mathemodus gesetzt; griechische Makros wie
  `\lambda` funktionieren unmittelbar.
- Die **Einheit** wird ohne `$...$` angegeben; sie wird automatisch in `[ ]`
  gesetzt und aufrecht dargestellt (z. B. `m/s^2`).
- Die **Bedeutung** dient zugleich als Label des Eintrags.

**Optionales Sortier-Argument.** In Sonderfällen – etwa bei identischen Zeichen mit
unterschiedlicher Bedeutung – lässt sich die Sortierung manuell steuern:

```latex
\newformulasymbol[optionalerSortierschluessel]{Bedeutung}{Zeichen}{Einheit}
```

Ohne dieses Argument sortiert die Vorlage automatisch nach dem Zeichen und löst
griechische Buchstaben über ein internes Wörterbuch normgerecht auf.

### 4.2 Symbole im Text verwenden

Wird ein eingetragenes Symbol über `\gls{<Bedeutung>}` referenziert, gibt die
Vorlage im **Mathemodus** das reine Symbol aus und im **Textmodus** Bedeutung und
Symbol. In der Praxis genügt es für die meisten Arbeiten, die Symbole schlicht
einzutragen – das Verzeichnis (Überschrift *Nomenklatur*) entsteht anschließend von
selbst.

### 4.3 Abkürzungen eintragen

Ebenfalls in `00-Symbole.tex`, über `\newacronym`:

```latex
% \newacronym[Optionen]{<Label>}{<Abkuerzung>}{<Langform>}
\newacronym{aoa}{aoa}{angle of attack}
\newacronym[plural=GKs,longplural={Genauigkeitsklassen}]{GK}{GK}{Genauigkeitsklasse}
\newacronym[description={Turbulente Grenzschicht}]{TBL}{TBL}{turbulente Grenzschicht}
```

- Im Text wird `\gls{Label}` verwendet (die erste Verwendung schreibt die Langform
  aus und ergänzt die Abkürzung in Klammern, danach erscheint nur noch die
  Abkürzung) sowie `\glspl{Label}` für den Plural.

> **Nicht löschen:** Am Ende von `00-Symbole.tex` steht `\glsaddall`. Diese Zeile
> stellt sicher, dass alle Einträge im Verzeichnis erscheinen – ohne sie bleibt das
> Verzeichnis leer.

---

## 5. Layout einsehen und anpassen

Sämtliche globalen Layout-Einstellungen befinden sich in
`misc/Background/Settings.tex`. Die folgenden Stellschrauben sind am häufigsten
relevant.

### 5.1 Seitenränder (Satzspiegel)

```latex
\usepackage[a4paper,tmargin=2cm, lmargin=3.2cm, rmargin=2cm, bmargin=3cm]{geometry}
```

Der linke Rand ist bewusst größer gewählt (Bindekorrektur). Daraus resultiert eine
Schreibbreite von rund 15,5 cm.

### 5.2 Absatzabstand statt Einrückung

Die Vorlage nutzt einen Abstand zwischen Absätzen ohne Erstzeilen-Einzug:

```latex
\setlength{\parindent}{0em}                      % Settings.tex
\setlength{\parskip}{18pt plus 2pt minus 1pt}    % gesetzt in Dokumentbeginn.tex
```

Absätze entstehen dadurch allein durch eine Leerzeile im Quellcode; ein manuelles
`\\` zur Abstandserzeugung ist nicht erforderlich.

### 5.3 Abstände der Überschriften

```latex
\titlespacing*{\section}{0pt}{12pt}{0pt}
\titlespacing*{\subsection}{0pt}{0pt}{0pt}
\titlespacing*{\subsubsection}{0pt}{0pt}{0pt}
```

Syntax: `{Abstand links}{Abstand davor}{Abstand danach}`.

### 5.4 Abstände in Listen

```latex
\setlist{itemsep=6pt, parsep=0pt, topsep=0pt, partopsep=0pt}
```

### 5.5 Schriftart und Zeilenabstand

Die Grundschrift ist eine skalierte Helvetica (`\sfdefault`); `mathastext` sorgt
für ein einheitliches Schriftbild im Mathemodus. Der Zeilenabstand lässt sich über
das (auskommentierte) `setspace`-Paket in `Settings.tex` aktivieren:

```latex
\usepackage[onehalfspacing]{setspace}  % Zeile einkommentieren fuer 1,5-fachen Abstand
```

### 5.6 Kopf- und Fußzeile

Konfiguriert über `fancyhdr` in `Dokumentbeginn.tex`: außen der Kapitelname
(kursiv, über `firstleftmark`), innen die Seitenzahl. Die Schriftgröße wird über
`\changefontbig` gesteuert.

### 5.7 Nummerierung

Gleichungen, Tabellen und Abbildungen werden kapitelweise gezählt
(`\numberwithin{...}{section}`). Der Vorspann nutzt römische Seitenzahlen, ab dem
ersten Kapitel arabische.

---

## 6. LaTeX Best Practices im Rahmen der Vorlage

- **Zentral pflegen:** Persönliche Daten ausschließlich in `Setup.tex`, Symbole und
  Abkürzungen ausschließlich in `00-Symbole.tex`. Niemals fest im Fließtext
  eintragen.
- **Bilder stets über `\newfigure`/`\newsvg`** einbinden und in `Bilder/` ablegen.
  Referenzen ausschließlich über `\autoref{fig:...}` setzen – so bleiben die
  Nummerierungen automatisch korrekt.
- **Einheiten stets über die Makros** aus `Einheitenmacros.tex` setzen. Das hält
  die Darstellung konsistent aufrecht und vermeidet kursive Einheiten.
- **Abstände nicht mit `\\` erzwingen.** Der globale `\parskip` erzeugt die
  Absatzabstände automatisch; ein Absatz entspricht einer Leerzeile im Code.
- **Floats kontrollieren** mit `\clearpage` (zwischen Kapiteln, bereits in
  `main.tex` vorhanden) und `\FloatBarrier` (nach Bildern automatisch gesetzt).
- **Kapitelweise arbeiten:** je eine Datei pro Kapitel, eingebunden über `\input`
  in `main.tex`. Das hält Kompilierzeiten und potenzielle Fehlerquellen gering.
- **Quellen sauber in `Literatur.bib`** pflegen und mit `\cite{key}` zitieren
  (Stil IEEE).
- **`misc/Background/` nicht anpassen**, solange nicht bewusst am Kern der Vorlage
  gearbeitet wird. Für eine gewöhnliche Arbeit ist dort keine Änderung nötig.
- **Vor umfangreichen Änderungen sichern** (Git-Commit oder Overleaf-Historie). Bei
  Problemen mit Verzeichnissen hilft häufig ein vollständiger Neu-Build inklusive
  Biber und makeglossaries.

---

## 7. Kompilier-Reihenfolge und Troubleshooting

### 7.1 Vollständiger Build

Ändern sich Literatur, Symbole oder Abkürzungen, genügt ein einzelner
pdfLaTeX-Lauf nicht. Die korrekte Reihenfolge lautet:

```
pdflatex main
biber main
makeglossaries main
pdflatex main
pdflatex main
```

Auf Overleaf übernimmt dies der *Recompile*-Button automatisch; bei hartnäckigen
Fehlern hilft *Menu → Clear cached files* mit anschließendem erneuten Lauf.

### 7.2 Häufige Stolpersteine

| Symptom | Ursache / Lösung |
|---|---|
| Symbol- oder Abkürzungsverzeichnis bleibt leer | `\glsaddall` gelöscht oder `makeglossaries`/xindy nicht ausgeführt |
| Fehlerhafte Zitate `[?]` | `biber`-Lauf fehlt oder BibTeX-Key falsch geschrieben |
| SVG wird nicht eingebunden | Shell-Escape/Inkscape fehlt (lokal `--shell-escape` aktivieren) |
| Kapitelname in Kopfzeile falsch | TeXLive-Version neuer als 2024 – gegebenenfalls auf 2024 zurücksetzen |
| Kompilierung bricht wegen fehlendem `\Titel` o. Ä. ab | Feld in `Settings.tex` versehentlich entfernt – erneut setzen |

### 7.3 Weiterentwicklung

Fehler oder Verbesserungsvorschläge bitte über das Issue-Template im Repository
melden: <https://github.com/TheSecretJas/Vorlage-Abschlussarbeit-HAW>.

