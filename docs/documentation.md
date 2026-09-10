
# Hintergrund

Wir haben auf unserer Webseite versucht, Kärtchen zu erstellen, um Problem Storys und deren Lösungen zur Datenqualität darzustellen. Die Kärtchen sind aufklappbar und enthalten Lösungen zu den jeweiligen Problem Storys. Allerdings war es nicht möglich mit einem normalen HTML Programm zu arbeiten, da wir eine Wordpress Seite haben. Um die gängigen Styles einzubauen, müsste man Extensions kaufen, die nicht Open-Source sind. Wir arbeiten schon mit mehreren Extensions, die immer wieder aktualisiert werden müssen, deswegen habe ich einen Workaround gefunden, um die Anwendung in unsere Wordpress Seite einzubauen, d.h. *drum rolls* inline-embed. Es gibt viele solche Workarounds, aber es hängt davon ab, was für einen Format ihr euch wünscht. In dieser Dokumentation beschreibe ich wie wir die Kärtchen einbauen konnten. 
Um den Code einzubauen, müsst ihr auf der Seite, die ihr bearbeitet, einen Block anlegen. In diesem Block, klickt ihr auch **individuelles HTML**. Ihr könnt den Quellcode von hier kopieren und in den Block einfügen.
![HTML-Block](../img/Screenshot%202026-08-27%20112056.png)

In dem Code gibt es ein Document-Object-Model (DOM). HTML ist eine statische Auszeichungssprache und ist nicht objektorientiert, d.h. es gibt kein klassisches Klassen-Objekt Modell. Es wird von dem Browser ins DOM umgewandelt. Das Objekt wäre also `<div>` oder `<details>` und die Objekte und jede Section der Seite hat eine `<Section Class>` wie z.B die Fußnoten. Es ist wichtig zu verstehen, wie das DOM funktioniert, damit man auch versteht, wie Seiten strukturiert werden.

## 1. Warum die Datei so aussieht, wie sie aussieht
 
Die Seite ist ein einziger Block Individuelles HTML in WordPress. Das hat einen Grund: In WordPress dürfen nur Administrator*innen sogenannte Stylesheets speichern – also ausgelagerte Gestaltungsanweisungen. Bei allen anderen Rollen werden sie beim Speichern kommentarlos entfernt (die Funktion dahinter heißt KSES). Wir ihr wisst, habe ich keine Admin-Rechte. Diese Dokumentation richtet sich eher an Menschen, die keine Admin-Rechte haben und deren Spielraum deswegen eingeschränkt ist. 
 
Daraus folgen drei Eigenheiten, die beim Lesen des Codes zunächst irritieren:
 
- **Jede Gestaltungsanweisung steht direkt am Element.** Deshalb wiederholt sich in jeder Karte dieselbe lange Schriftdefinition. Mit einem Stylesheet wäre die Datei etwa ein Viertel so groß – dafür würde sie in WordPress nicht funktionieren.
- **Es gibt kein JavaScript.** Das Auf- und Zuklappen erledigt der Browser selbst über ein HTML-Element namens `<details>`.
- **Alle Verknüpfungen sind Sprungmarken.** Es gibt keine Filterfunktion, sondern ein Register am Seitenende, auf das die Schlagwörter verweisen.
> **Wenn sich die Rechtelage ändert:** Sobald jemand mit Administrator-Rechten das Design zentral hinterlegen kann (unter *Design → Customizer → Zusätzliches CSS*), ließe sich die Datei drastisch verschlanken und um Komfortfunktionen erweitern – etwa den Textwechsel „Weiterlesen / Weniger anzeigen". Das ist eine einmalige Aufgabe von etwa zehn Minuten.
 
---
 
## 2. Wie die Seite aufgebaut ist
 
```
Einleitungskasten            Text + aufklappbarer Teil + zwei Fußnoten
Kapitelmenü                  10 Schaltflächen (9 Kapitel + Register)
Kapitel 1 … 9                je eine Überschrift + eine Reihe Karten
Trennlinie
Schlagwortregister           46 Einträge, alphabetisch
```
 
Die Kapitel und ihre Farben:
 
| Nr. | Kapitel | Farbe | Stories |
|-----|---------|-------|---------|
| 1 | Qualitätskontrolle | `#1C6F6A` Petrol | 1 |
| 2 | Datenbereinigung | `#2E7A4E` Grün | 1 |
| 3 | Heterogenität & Inkonsistenz | `#B0432B` Ziegelrot | 3 |
| 4 | Unsicherheiten | `#AE7712` Ocker | 4 |
| 5 | Maschinenlesbarkeit | `#1F7BA6` Blau | 5 |
| 6 | Standardisierung & kontrollierte Vokabulare | `#9A3465` Beere | 8 |
| 7 | Tools | `#5C6E22` Oliv | 2 |
| 8 | Ethik & Objektivität | `#6A4CA0` Violett | 2 |
| 9 | Datenschutz | `#33488E` Indigo | 1 |
 
Die Farbe gehört zum Thema, nicht zur Position. Wird ein Kapitel verschoben, wandert seine Farbe mit.
 
---
 
## 3. Das Nötigste über HTML
 
Nur vier Begriffe, dann ist der Code lesbar.
 
**Tag.** Eine Anweisung in spitzen Klammern. Fast jedes Tag kommt im Paar: `<p>` öffnet einen Absatz, `</p>` schließt ihn. Der Schrägstrich markiert das Ende. Wird ein Tag nicht geschlossen, verrutscht in aller Regel der Rest der Seite.
 
**Attribut.** Eine Zusatzangabe innerhalb des öffnenden Tags, in Anführungszeichen:
 
```html
<a href="#kapitel-1">Qualitätskontrolle</a>
   └ Attribut ┘└ Ziel ┘ └ sichtbarer Text ┘
```
 
**Verschachtelung.** Tags liegen ineinander wie Schachteln und dürfen sich nicht überkreuzen. Richtig ist `<p><em>Text</em></p>`, falsch `<p><em>Text</p></em>`.
 
**Sprungmarke.** Ein `id`-Attribut benennt eine Stelle, ein `href` mit Raute springt dorthin. Beide Schreibweisen müssen exakt übereinstimmen, Groß- und Kleinschreibung eingeschlossen.
 
Alles, was nicht in spitzen Klammern steht, ist sichtbarer Text und darf gefahrlos geändert werden.
 
---
 
## 4. Aufbau einer Problem Story
 
Hier eine Karte im Rohbau – die langen `style="…"`-Angaben sind weggelassen, sie enthalten nur Schriftgrößen und Farben:
 
```html
<div id="ps-1-1" style="…">                     ← die Karte, Sprungziel aus dem Register
 
  <div style="…">
    <span style="…">1.1</span>                   ← Nummer
    <span style="…">Qualitätskontrolle</span>    ← Rubrik
    <h3 style="…">Quality Control First</h3>     ← Titel
  </div>
 
  <div style="…">
    <p style="…">Wir arbeiten mit einem …</p>    ← Problem, immer sichtbar
    <details class="ps-mehr">                    ← optionale Fortsetzung
      <summary style="…">weiterlesen</summary>
      <div style="…"><p style="…">…</p></div>
    </details>
  </div>
 
  <div style="margin-top:auto">                  ← Fußbereich, sitzt immer unten
    <div style="…">
      <p style="…">Datenqualitätsproblem</p>
      <p style="…">fehlende Qualitätskontrolle im Projekt</p>
    </div>
    <details class="ps-loesung" style="…">       ← Lösung, aufklappbar
      <summary style="…">Lösung ansehen</summary>
      <div style="…">
        <p style="…">Je nach Arbeitsumgebung …</p>
        <p style="…">Schlagwörter</p>
        <p><a href="#tag-…" style="…">Qualitätskontrolle</a> …</p>
        <p style="…">Weiterführende Links</p>
        <ul style="…"><li style="…">… <a href="…">…</a></li></ul>
      </div>
    </details>
  </div>
 
</div>
```
 
Zwei Mechanismen lohnen das Verständnis:
 
**Das Aufklappen.** `<details>` und `<summary>` sind Standard-HTML. Das erste `<summary>` ist die Beschriftung, alles Weitere der verborgene Inhalt. Es braucht keine Verknüpfung – die Position im Code genügt. Wichtig ist nur, dass `<summary>` unmittelbar im `<details>` steht.
 
**Der bündige Fußbereich.** Die Angabe `margin-top:auto` schiebt den Fuß nach unten, sodass „Lösung ansehen" in allen Karten einer Reihe auf gleicher Höhe sitzt, egal wie lang die Problembeschreibung ist. Nicht anfassen – sonst franst das Raster aus.
 
**Nicht alle Bausteine sind Pflicht.** Der Block `ps-mehr` und der Abschnitt „Weiterführende Links" fehlen in manchen Karten. Das ist Absicht und kein Fehler.
 
---
 
## 5. Wiederkehrende Handgriffe
 
### 5.1 Text ändern
 
Den Text zwischen den Tags überschreiben, Tags stehen lassen. Für Ergänzungen im laufenden Text drei Regeln:
 
| Zeichen | Schreibweise | Grund |
|---------|--------------|-------|
| kaufmännisches Und | `&amp;` | einzelnes `&` kann Folgezeichen verschlucken |
| Anführungszeichen | `&bdquo;` … `&ldquo;` | ergibt „so“ statt "so" |
| Gedankenstrich | `&ndash;` | ergibt – statt - |
| Abkürzungen | `z.&nbsp;B.` | verhindert Umbruch zwischen z. und B. |
 
Für Kursivsetzung – etwa bei Werktiteln – `<em>Titel</em>`.
 
### 5.2 Eine neue Problem Story ergänzen
 
1. Eine bestehende Karte desselben Kapitels **vollständig** kopieren, von `<div id="ps-…"` bis zum zugehörigen `</div>`. Am einfachsten mit der Suchfunktion des Editors: nach `id="ps-4-2"` suchen und ab dort bis zum Beginn der nächsten Karte markieren.
2. Die Kopie direkt vor das `</div>` einfügen, das die Kartenreihe des Kapitels beendet.
3. Nummer und `id` anpassen: aus `4.4` wird `4.5`, aus `id="ps-4-4"` wird `id="ps-4-5"`.
4. Titel, Problem, Datenqualitätsproblem und Lösung überschreiben.
5. Schlagwörter anpassen (siehe 5.3) und den Zähler im Kapitelmenü erhöhen.
Farben müssen nicht geändert werden, solange die Karte im selben Kapitel bleibt – sie sind in der Vorlage bereits richtig.
 
### 5.3 Schlagwörter ändern
 
Jedes Schlagwort existiert an zwei Stellen: als Chip in der Karte und als Eintrag im Register. Beide müssen zusammenpassen, sonst laufen Links ins Leere.
 
**Vorhandenes Schlagwort einer Karte zuweisen.** Chip aus einer anderen Karte kopieren, dabei die Farbe an das Kapitel anpassen (drei Stellen: `color:`, `border:` und die Farbe im Rahmen). Dann im Register beim betreffenden Eintrag einen Nummern-Chip mit der neuen Kartennummer ergänzen.
 
**Neues Schlagwort anlegen.** Zusätzlich im Register einen neuen `<li>`-Eintrag an alphabetisch passender Stelle einfügen. Die `id` folgt festen Regeln: alles klein, Leerzeichen werden zu Bindestrichen, Umlaute ausgeschrieben.
 
| Schlagwort | id |
|------------|-----|
| Dokumentation | `tag-dokumentation` |
| Qualitätskontrolle | `tag-qualitaetskontrolle` |
| kontrollierte Vokabulare | `tag-kontrollierte-vokabulare` |
| Boolesche Werte | `tag-boolesche-werte` |
 
Zuletzt den Zähler am Register-Eintrag im Kapitelmenü aktualisieren.
 
> Diese Doppelpflege ist der wundeste Punkt der Konstruktion. Wenn absehbar viele Stories dazukommen, lohnt es sich, das Register maschinell erzeugen zu lassen, statt es von Hand zu führen.
 
### 5.4 Einen weiterführenden Link ergänzen
 
Innerhalb der Liste am Kartenende ein `<li>` kopieren und anpassen. Der Linktext sollte die vollständige URL wiederholen – bei Literaturangaben üblich, weil die Referenz auch im Ausdruck vollständig bleiben soll:
 
```html
<li style="…;overflow-wrap:anywhere">Nachname, V. (Jahr). <em>Titel.</em> Zenodo.
<a href="https://doi.org/…" target="_blank" rel="noopener">https://doi.org/…</a>.</li>
```
 
`target="_blank"` öffnet einen neuen Tab, `rel="noopener"` gehört aus Sicherheitsgründen immer dazu. `overflow-wrap:anywhere` sorgt dafür, dass lange URLs auf schmalen Bildschirmen umbrechen statt aus der Karte zu laufen.
 
### 5.5 Ein Kapitel umbenennen
 
An drei Stellen ändern: in der Kapitelüberschrift, im Kapitelmenü oben und in der Rubrikzeile jeder Karte dieses Kapitels. Die `id` (`kapitel-4`) bleibt unverändert – sie ist nur eine technische Adresse und muss nicht zum Titel passen.
 
---
 
## 6. Vor dem Veröffentlichen prüfen
 
- [ ] Die Seite in der **Vorschau** ansehen, nicht nur im Editor – `<details>` klappt im Editor nicht zuverlässig auf
- [ ] Alle geänderten Karten einmal auf- und zuklappen
- [ ] Jeden neuen Link anklicken
- [ ] Vom Kapitelmenü in jedes geänderte Kapitel springen
- [ ] Ein geändertes Schlagwort anklicken und vom Register aus zurückspringen
- [ ] Die Seite auf dem Handy ansehen – oder das Browserfenster schmal ziehen
- [ ] Prüfen, ob die Zähler im Kapitelmenü noch stimmen
**Sicherungskopie:** Vor größeren Änderungen den kompletten Inhalt des HTML-Blocks in eine Textdatei kopieren und mit Datum ablegen. WordPress führt zwar Revisionen, aber der Rückweg über einen 206 KB großen Block ist unangenehm.
 
---
 
## 7. Häufige Fehler
 
| Symptom | Ursache |
|---------|---------|
| Ab einer Stelle rutscht das Layout | Ein Tag nicht geschlossen oder in falscher Reihenfolge |
| Gestaltung fehlt ab einer Stelle | Ein Anführungszeichen im `style`-Attribut fehlt |
| Ein Klick auf ein Schlagwort tut nichts | `href` und `id` stimmen nicht überein (Umlaut, Groß-/Kleinschreibung) |
| Der Sprung landet unter dem Seitenkopf | `scroll-margin-top` fehlt am Ziel |
| Code erscheint als sichtbarer Text | `<style>` oder `<script>` verwendet – wird beim Speichern entfernt |
| Tags werden angezeigt statt ausgeführt | Der Text steht in einem Absatz-Block statt im Block Individuelles HTML |
 
Ein Editor mit Syntaxhervorhebung – etwa Visual Studio Code – markiert fehlende Klammern und Anführungszeichen sofort farbig. Für längere Bearbeitungen ist das die deutlich sicherere Umgebung als das WordPress-Textfeld.
 
---
 
## 8. Was bewusst nicht geht
 
Damit niemand vergeblich sucht:
 
- **Filtern nach Schlagwort.** Bräuchte JavaScript. Ersatz ist das Register.
- **Suchfeld.** Ebenso. Die Browsersuche (Strg+F) findet allerdings nur aufgeklappte Inhalte.
- **Alle Karten gleichzeitig aufklappen.** Ebenso.
- **Textwechsel „Weiterlesen / Weniger anzeigen".** Bräuchte ein Stylesheet. Der Pfeil des Browsers zeigt den Zustand.
Alle vier wären mit einmaligem Administrator-Zugriff möglich. Solange der fehlt, ist die aktuelle Konstruktion die tragfähigste Lösung: Sie funktioniert ohne Zusatzrechte, ohne Plugin und ohne externe Abhängigkeiten – und bleibt lesbar, wenn Gestaltung verlorengeht.
 