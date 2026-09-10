
# Hintergrund

Wir haben auf unserer Webseite versucht, Kärtchen zu erstellen, um Problem Storys und deren Lösungen zur Datenqualität darzustellen. Die Kärtchen sind aufklappbar und enthalten Lösungen zu den jeweiligen Problem Storys. Allerdings war es nicht möglich mit einem normalen HTML Programm zu arbeiten, da wir eine Wordpress Seite haben. Um die gängigen Styles einzubauen, müsste man Extensions kaufen, die nicht Open-Source sind. Wir arbeiten schon mit mehreren Extensions, die immer wieder aktualisiert werden müssen, deswegen habe ich einen Workaround gefunden, um die Anwendung in unsere Wordpress Seite einzubauen, d.h. *drum rolls* inline-embed. Es gibt viele solche Workarounds, aber es hängt davon ab, was für einen Format ihr euch wünscht. In dieser Dokumentation beschreibe ich wie wir die Kärtchen einbauen konnten. 
Um den Code einzubauen, müsst ihr auf der Seite, die ihr bearbeitet, einen Block anlegen. In diesem Block, klickt ihr auch **individuelles HTML**. Ihr könnt den Quellcode von hier kopieren und in den Block einfügen.
![HTML-Block](../img/Screenshot%202026-08-27%20112056.png)

In dem Code gibt es ein Document-Object-Model (DOM). HTML ist eine statische Auszeichungssprache un ist nicht objektorientiert, d.h. es gibt kein klassisches Klassen-Objekt Modell. Es wird von dem Browser ins DOM umgewandelt. Das Objekt wäre also "div" oder "details" und die Objekte und jede Section der Seite hat eine "Section Class" wie z.B die Fußnoten. Es ist wichtig zu verstehen, wie das DOM funktioniert, damit man auch versteht, wie Seiten strukturiert werden.

# Styles

Wir können leider auf Wordpress keine CSS-gestützte Styles verwenden. Deswegen habe ich **inline styles** eingebaut.

```html
<div class="ps-wrap" style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;color:#0B2430;line-height:1.55;max-width:1120px;margin:0 auto">
<div style="border-top:5px solid #004F6E;border-right:1px solid #D7DEE1;border-bottom:1px solid #D7DEE1;border-left:1px solid #D7DEE1;border-radius:4px;background-color:#FFFFFF;padding:26px 28px 28px;margin:0 0 26px">
<p style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:16px;line-height:1.6;color:#415563;margin:0 0 10px;max-width:60em">Diese Sammlung bietet einen praxisnahen Einstieg in den Umgang mit strukturierten Daten in der Geschichtsforschung. Sie stellt typische Herausforderungen zusammen, denen man bei der Arbeit mit unterschiedlichen Datentypen begegnet, und zeigt anwendbare Lösungswege auf. Jedes Fallbeispiel – die sogenannte Problem Story – folgt demselben Aufbau:</p>
<ol style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:16px;line-height:1.6;color:#415563;margin:0 0 16px;max-width:60em">;
```

Wie ihr seht, habe ich in den **div classes** den Font und Farbe des obersten Blocks festgelegt. Die Rahmen habe ich mit **div style** festgelegt.
```html
<div style="border-top:5px solid #004F6E;border-right:1px solid #D7DEE1;border-bottom:1px solid #D7DEE1;border-left:1px solid #D7DEE1;border-radius:4px;background-color:#FFFFFF;padding:26px 28px 28px;margin:0 0 26px">;
```

Für Inline Styles müsst ihr die Styles in den Code einbauen, wenn ihr auf Wordpress eine HTML-Anwendung einbetten möchtet. Ansonsten braucht ihr eine CSS Extension oder ihr seht den rohen Code auf der Seite, wenn ihr sie veröffentlicht. Die Styles sind die größten Hürden, wenn man einen individuellen HTML Codeblock einbettet.

Die Styles habe ich wieder in den Absätzen verwendet. Mit *<p style>*
```html
<details style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:16px;line-height:1.6;color:#415563;max-width:60em"><summary style="cursor:pointer;font-weight:600;color:#004F6E">Weiterlesen</summary><div style="margin-top:12px">
<p style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:16px;line-height:1.6;color:#415563;margin:0 0 10px;max-width:60em">Die Beispiele stammen aus der Beratungspraxis der NFDI4Memory FAIR Data Fellowships<sup id="fnref1"><a href="#fn1">1</a></sup>, den Ergebnissen der Umfrageauswertung „Praktiken, Standards und Bedarfe zur Datenqualität in den Communities der historisch arbeitenden Fächer“<sup id="fnref2"><a href="#fn2">2</a></sup> und den alltäglichen Erfahrungen unserer Arbeitsbereiche. Wo die Beispiele auf realen Projekten basieren, wurden die Geschichten von den Autor*innen umformuliert. Einige Fallbeispiele berühren zudem übergreifende methodische Fragen, wie die Qualitätskontrolle oder das Streben nach Objektivität bei der Datenbereinigung. Diese sind für die gesamte historische Arbeit relevant, jedoch insbesondere für strukturierte Daten.</p>
<p style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:16px;line-height:1.6;color:#415563;margin:0 0 10px;max-width:60em">Das Angebot richtet sich gezielt an Forschende, die in ihrer Arbeit mit strukturierten Daten wie Tabellen zu tun haben, sich aber noch nicht intensiv mit dem Forschungsdatenmanagement auseinandergesetzt haben. Um die Hürden so niedrig wie möglich zu halten, sind die Problemstellungen bewusst konkret gewählt. Die Lösungsvorschläge hingegen sind bewusst allgemein gehalten, damit man sie unabhängig vom eigenen Thema oder Vorwissen direkt nutzen kann.</p>
<p style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:16px;line-height:1.6;color:#415563;margin:0 0 10px;max-width:60em">Uns ist bewusst, dass es für fast jede dieser Situationen auch technisch komplexere Lösungen gibt. Ziel dieser Sammlung ist es jedoch nicht, tiefgehende IT-Expertise zu vermitteln, sondern schnelle „Erste Hilfe“ zu leisten und die Orientierung für die nächsten Schritte zu erleichtern.</p>
</div></details>
```

# Filter System

Ein Feature unserer Seite ist natürlich das Filtersystem. Ich habe jedes Problem nach Farbe kodiert und mit die Problem Storys dementsprechend kategorisiert.

```html
<p style="margin:0 0 26px">
<a href="#kapitel-1" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #1C6F6A;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Qualitätskontrolle <span style="color:#1C6F6A;font-weight:700">1</span></a>
<a href="#kapitel-2" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #2E7A4E;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Datenbereinigung <span style="color:#2E7A4E;font-weight:700">1</span></a>
<a href="#kapitel-3" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #B0432B;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Heterogenität &amp; Inkonsistenz <span style="color:#B0432B;font-weight:700">3</span></a>
<a href="#kapitel-4" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #AE7712;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Unsicherheiten <span style="color:#AE7712;font-weight:700">4</span></a>
<a href="#kapitel-5" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #1F7BA6;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Maschinenlesbarkeit <span style="color:#1F7BA6;font-weight:700">5</span></a>
<a href="#kapitel-6" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #9A3465;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Standardisierung &amp; kontrollierte Vokabulare <span style="color:#9A3465;font-weight:700">8</span></a>
<a href="#kapitel-7" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #5C6E22;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Tools <span style="color:#5C6E22;font-weight:700">2</span></a>
<a href="#kapitel-8" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #6A4CA0;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Ethik &amp; Objektivität <span style="color:#6A4CA0;font-weight:700">2</span></a>
<a href="#kapitel-9" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #33488E;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Datenschutz <span style="color:#33488E;font-weight:700">1</span></a>
<a href="#schlagwortregister" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #004F6E;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Schlagwortregister <span style="color:#004F6E;font-weight:700">46</span></a>
</p>
```
Der vorliegende Code zeigt, dass wir die Buttons von den jeweiligen Problemen schon am Anfang stylen müssen. Der Syntax sieht genau so aus:
```html
<a href="kapitel-n" style=">style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:12px;color:#415563;text-decoration:none;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:4px solid #004F6E;border-radius:3px;padding:5px 11px;margin:0 6px 6px 0">Titel <span style="color:#004F6E;font-weight:700">46</span></a>
```

Jetzt müssen wir die Kärtchen mit den Buttons verknüpfen. Das funktioniert so:
```html
<h2 id="kapitel-1" style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:15px;font-weight:600;letter-spacing:1px;text-transform:uppercase;color:#1C6F6A;border-bottom:2px solid #1C6F6A;padding-bottom:8px;margin:34px 0 16px">1. Qualitätskontrolle</h2>
<div style="display:flex;flex-wrap:wrap;align-items:stretch;gap:18px">

<div id="ps-1-1" style="flex:1 1 320px;max-width:560px;background-color:#FFFFFF;border:1px solid #D7DEE1;border-left:5px solid #1C6F6A;border-radius:4px;overflow:hidden;display:flex;flex-direction:column"><div style="padding:14px 18px 0"><span style="font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:13px;font-weight:700;color:#1C6F6A">1.1</span><span style="font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:11px;letter-spacing:1px;text-transform:uppercase;color:#415563;margin-left:10px">Qualitätskontrolle</span><h3 style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:19px;font-weight:600;line-height:1.25;color:#0B2430;margin:8px 0 10px;min-height:48px">Quality Control First</h3></div><div style="padding:0 18px 14px;min-height:84px"><p style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:15px;line-height:1.6;color:#243642;margin:0">Wir arbeiten mit einem großen Team an einem Projekt und verwenden oft unterschiedliche Bezeichnungen für dieselben Dinge. Das führt zu Verwirrung und erschwert unsere Arbeit.</p></div><div style="margin-top:auto"><div style="padding:10px 18px 12px;background-color:#1C6F6A08;border-top:1px solid #D7DEE1"><p style="font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:10px;letter-spacing:1.5px;text-transform:uppercase;color:#1C6F6A;margin:0 0 4px">Datenqualitätsproblem</p><p style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:13px;line-height:1.4;color:#415563;margin:0">fehlende Qualitätskontrolle im Projekt</p></div><details class="ps-loesung" style="padding:14px 18px 16px;background-color:#1C6F6A0F;border-top:1px solid #D7DEE1"><summary style="font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:11px;letter-spacing:1.5px;text-transform:uppercase;font-weight:600;color:#1C6F6A;cursor:pointer">Lösung ansehen</summary><div style="margin-top:12px"><p style="font-family:system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif;font-size:14px;line-height:1.55;color:#0B2430;margin:0 0 10px">Je nach Arbeitsumgebung und genutzten Anwendungen sollte das Projektteam möglichst schon zum Projektstart auf kontrollierte Vokabulare zurückgreifen und diese beispielsweise als feste Wertelisten in Tabellen oder Tools für das Projektmanagement hinterlegen. Bei Bedarf kann eine einfache projektinterne Liste für die einheitliche Bezeichnung von einzelnen Arbeitsschritten und -ständen schon hilfreich sein. Spätestens bei der strukturierten Erschließung, Indexierung oder Annotation von Forschungsdaten und Informationsobjekten jeder Art sollte auf kontrollierte Vokabulare zurückgegriffen werden. Um die Datenqualität im Projektverlauf zu sichern, ist es sinnvoll, verbindliche Qualitätskontrollen und entsprechende Prozesse zur Korrektur zu vereinbaren und zu etablieren.</p><p style="font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:10px;letter-spacing:1.5px;text-transform:uppercase;color:#1C6F6A;margin:14px 0 6px">Schlagwörter</p><p style="margin:0"><a href="#tag-qualitaetskontrolle" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:11px;color:#1C6F6A;background-color:#FFFFFF;border:1px solid #1C6F6A59;border-radius:20px;padding:2px 9px;margin:0 4px 4px 0;text-decoration:none">Qualitätskontrolle</a><a href="#tag-zusammenarbeit" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:11px;color:#1C6F6A;background-color:#FFFFFF;border:1px solid #1C6F6A59;border-radius:20px;padding:2px 9px;margin:0 4px 4px 0;text-decoration:none">Zusammenarbeit</a><a href="#tag-dokumentation" style="display:inline-block;font-family:ui-monospace,Consolas,Menlo,'Courier New',monospace;font-size:11px;color:#1C6F6A;background-color:#FFFFFF;border:1px solid #1C6F6A59;border-radius:20px;padding:2px 9px;margin:0 4px 4px 0;text-decoration:none">Dokumentation</a></p></div></details></div></div>
</div>
```

# Die Verschachtelung 

Ein Feature des Codes ist die Verschachtelung im Rahmen des DOM. Der Block besteht aus vier ineinandergeschachtelten Ebenen:

``` html
<h2 id="kapitel-1">          
<div display:flex>           
  └ <div id="ps-1-1">        
      ├ Kopf: Nummer, Rubrik, Titel
      ├ Problembeschreibung
      └ <div margin-top:auto> 
          ├ Datenqualitätsproblem
          └ <details>
```

## Die Zeile:
display:flex mit flex-wrap:wrap legt die Karten nebeneinander und bricht um, wenn der Platz nicht reicht. gap:18px setzt den Abstand – ohne Randmargen, die sich addieren würden. align-items:stretch sorgt dafür, dass alle Karten einer Reihe gleich hoch werden, unabhängig von der Textmenge.

## Die Karte:
 flex:1 1 320px ist die Kurzschreibweise für drei Werte: wachsen darf sie (1), schrumpfen auch (1), und ihre Ausgangsbreite beträgt 320 px. Zusammen mit max-width:560px ergibt das ein responsives Verhalten ohne Media Queries – auf breiten Bildschirmen zwei Karten nebeneinander, auf dem Handy eine.

## Der Trick mit dem Fuß:
Die Karte ist selbst wieder display:flex mit flex-direction:column, also eine vertikale Box. Der Fußbereich hat margin-top:auto, was den verbleibenden Leerraum komplett über ihn schiebt. Effekt: „Lösung ansehen" sitzt in allen Karten auf gleicher Höhe am unteren Rand, auch wenn die Problemtexte unterschiedlich lang sind. Die min-height-Werte (48px beim Titel, 84px beim Problemtext) machen dasselbe für die obere Hälfte.

## Die Farben:
#1C6F6A ist das Petrol dieses Kapitels. Auffällig sind die achtstelligen Varianten: #1C6F6A08 hängt zwei Stellen für die Deckkraft an – 08 sind rund 3 %, 0F etwa 6 %, 59 rund 35 %. So entstehen die zarten Hintergrundflächen und die halbtransparenten Rahmen der Schlagwort-Chips aus einer einzigen Grundfarbe, ohne zusätzliche Farbwerte definieren zu müssen.

## Das Aufklappen. 
<details> mit <summary> ist ein natives HTML-Element – der Browser übernimmt Öffnen und Schließen, Tastaturbedienung und Screenreader-Ansage von selbst. Genau deshalb funktioniert die Seite ohne eine Zeile JavaScript, was in deinem WordPress ja die entscheidende Einschränkung war.

## Die Anker:
 id="kapitel-1" ist das Ziel des Menüs oben, id="ps-1-1" das Ziel der Nummern-Chips im Register, und die Schlagwörter sind ihrerseits <a href="#tag-…"> zurück ins Register. Drei Verweisrichtungen, alle über reine Fragment-Links.

Der Preis dieser Bauweise ist die Redundanz: Jede Schriftdefinition steht ausgeschrieben in jedem Element. Mit einem Stylesheet wären es 46 KB statt 400. Für die WordPress-Situation ist es trotzdem der richtige Weg.

# Die Lösung ansehen - über die Verschachtelung

``` html
<details>
  <summary>Lösung ansehen</summary>   
  <div>…Inhalt…</div>                 
</details>
```
Die Regel lautet: Das erste <summary> innerhalb eines <details> ist die Beschriftung, alle übrigen Kindelemente bilden den Inhalt. Kein id, kein for, kein aria-controls nötig – der Browser leitet das aus der Struktur ab. Deshalb ist es auch wichtig, dass <summary> wirklich direkt darin steht und nicht in einem <div> verpackt ist; dann verlöre es seine Funktion und wäre nur noch Text.

Beim Klick setzt der Browser das Attribut open auf das <details> und blendet den Rest ein. Genau daran wollten wir früher den Textwechsel „Weiterlesen / Weniger anzeigen" festmachen – details[open] – was ohne Stylesheet nicht ging.

Das cursor:pointer im style des <summary> ist reine Kosmetik: Es macht aus dem Textcursor einen Zeigefinger. Klickbar wäre das Element auch ohne.

# Die Kapitel-Chips oben

Die sehen wie Buttons aus, sind aber gewöhnliche Links. Verknüpft wird über den Fragmentbezeichner: 

``` html
<a href="#kapitel-1">Qualitätskontrolle 1</a>   
…
<h2 id="kapitel-1">1. Qualitätskontrolle</h2>
```
Der Text nach der Raute muss exakt dem id-Wert entsprechen, Groß- und Kleinschreibung inklusive. Der Button-Look entsteht allein durch display:inline-block plus border, padding und border-radius – ein <a> ist standardmäßig inline und würde padding sonst nur unsauber darstellen.

Nach demselben Prinzip arbeiten auch die Schlagwörter (#tag-dokumentation) und die Nummern-Chips im Register (#ps-1-1). Alle drei Verweisarten sind reine Anker – deshalb überstehen sie die KSES-Filterung, die dir <style> weggeputzt hat.





