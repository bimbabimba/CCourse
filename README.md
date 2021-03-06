<!--

author:   Sebastian Zug & André Dietrich & Galina Rudolf
email:    sebastian.zug@informatik.tu-freiberg.de & andre.dietrich@ovgu.de & Galina.Rudolf@informatik.tu-freiberg.de
version:  1.0.1
language: de
narrator: Deutsch Female

comment: C-Kurs für Nicht-Informatiker 
logo: ./img/LogoCodeExample.png

import: https://raw.githubusercontent.com/LiaTemplates/Rextester/master/README.md

-->

# C-Kurs

![C logo](img/logo.png)

See the interactive version at
[https://LiaScript.github.io](https://LiaScript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/README.md)

Der vorliegende C-Kurs wird seit dem Wintersemester 2018/19 an der TU Bergakademie
Freiberg für die Veranstaltung "Prozedurale Programmierung" genutzt und auf der Basis von LiaScript realisiert. Die
Veranstaltung richtet sich an Nicht-Informatiker aus verschiedenen
ingenieurwissenschaftlichen Disziplinen mit keinen oder geringen
Programmierkenntnissen. Kern der Lösung ist die Möglichkeit Code direkt in der
Webseite auszuführen und auch Änderungen vorzunehmen, die dann in einem
"Versionssystem light" verfügbar sind.

Basis für die Ausführungsumgebung ist die API von Rextester https://rextester.com/. Vielen Dank für diesen Service!

Ausführbarer C Code sieht wie folgt aus, der Titel kann weggelassen werden.

```cpp                     HelloWorld.c
#include <stdio.h>

int main() {
	printf("Hello World\n");
	return 0;
}
```
@Rextester.C

Der obligatorische Markdown-Quellcodeblock wird durch um den Makroaufruf `@Rextester.C` am
Ende ergänzt. Dabei können unterschiedliche Compiler (gcc, clang, Microsoft C Compiler) und Parametersets genutzt werden.

```
@Rextester.C
@Rextester.C_clang
@Rextester.C_vc
@Rextester.C(true,`@input(1)`)
@Rextester.eval(@C, false, ,`-Wall -std=gnu99 -O2 -o a.out source_file.c`)
```

Der zweite Parameter gibt an, ob die Rückgaben der Rextester-Ausführungsumgebung
auf dem Bildschirm angezeigt werden sollen. Der Aufruf des vorhergehenden Code-Samples
mit `@Rextester.C(true, )` generiert eine knappe Statistik der Kompilierung
und der Ausführungsparameter.

```cpp                     HelloWorld.c
#include <stdio.h>

int main() {
	printf("Hello World\n");
	return 0;
}
```
@Rextester.C(true, )

Das folgende Beispiel `@Rextester.C(false,`@input(1)`)` illustriert die Übergabe von Argumenten über die "Commandozeile".

```cpp                     GetChar.c
#include <stdio.h>

int main(){
	char c;
	printf("Mit welchem Buchstaben beginnt ihr Vorname? ");
	c = getchar();
	printf("\nIch weiss jetzt, dass Ihr Vorname mit '%c' beginnt.\n", c);
	return 0;
}
```
``` text                  stdin
T
```
@Rextester.C(false,`@input(1)`)

Fehlerausgaben werden entsprechend der Compiler-Implementierung wie folgt generiert:

```cpp                     ErroneousHelloWorld.c
#include <stdio.h>

int main() {
	printf("Hello World\n")
	return 0;
}
```
@Rextester.C_clang(true, )

# Prozedurale Programmierung (WS 2019/20)

**Dozenten**

| Name             | Email                                      |
|:---------------- |:------------------------------------------ |
| Sebastian Zug    | sebastian.zug@informatik.tu-freiberg.de    |
| Galina Rudolf    | galina.rudolf@informatik.tu-freiberg.de    |
| Martin Reinhardt | martin.reinhardt@informatik.tu-freiberg.de |
| Alexander Buhl   | alexander.buhl@student.tu-freiberg.de      |

**Zielstellung der Veranstaltung**

* Grundlegendes Verständnis von (hardwarenaher) Programmierung
* Elementare Fähigkeiten in der Programmiersprache C
* Anwendung von Programmiertools im Entwicklungsprozess
* Systematischer Entwurf von Algorithmen

**Zeitaufwand und Engagement**

Der Zeitaufwand beträgt 180h und setzt sich zusammen aus 60h Präsenzzeit und
120h Selbststudium. Letzteres umfasst die Vor- und Nachbereitung der
Lehrveranstaltungen, die eigenständige Lösung von Übungsaufgaben sowie die
Prüfungsvorbereitung.

# Literaturempfehlungen

Der Kurs selbst ist unter

https://github.com/SebastianZug/CCourse

verfügbar. Diese können entweder in der Markdown-Syntax oder als Interaktives
Dokument betrachtet werden.

Achtung! Es handelt sich um "lebende" Materialien.

**Online Kurse**

* [The GNU C Reference Manual](https://www.gnu.org/software/gnu-c-manual/gnu-c-manual.html)
* Wolf, J., _"C von A bis Z"_, Rheinwerk Verlag
  [Link](http://openbook.rheinwerk-verlag.de/c_von_a_bis_z/000_c_vorwort_001.htm#mj764cb3fd439d3b95d1843e7c7d17f235)
* C Kurs Universität Chemnitz,
  [Link](https://www.tu-chemnitz.de/urz/archiv/kursunterlagen/C/index.htm)

**Videotutorials**

* Vorlesung Prof. Dr. Justus Piater, Universität Insbruck 2014
  [YouTube](https://www.youtube.com/watch?v=7P7dSOKAonM)
* Reihe von Tutorials zu verschiedenen Veranstaltungen der Goethe Universität
  Frankfurt [YouTube](https://www.youtube.com/watch?v=CeEfTlRFEA0&t=210s)

**Bücher**

* Kernighan B.W., Ritchie D.M., _"Programmieren in C"_, Hanser Verlag
* Prinz P., Crawford T., _"C in a Nutshell"_, O'Reilly
* Wolf J., _"Grundkurs C"_, Rheinwerk Computing

# Vorlesungsinhalte

| Datum      | Inhalt                                                                                                                                                                   |
|:---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 14.10.2019 | [1.  Einführung](https://LiaScript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/01_Einfuehrung.md)                                       |
| 21.10.2019 | [2. Variablen und Datentypen, Ein- und Ausgabe](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/02_Grundlagen.md#1)       |
| 28.10.2019 | [3. Operatoren](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/03_Operatoren.md#1)                                       |
|  4.11.2019 | [4. Kontrollstrukturen](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/04_Kontrollstrukturen.md#1)                       |
| 11/18.11.2019 | [5. Komplexe Datentypen](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/05_ZusammengesetzteDatentypen.md#1)              |
| 25.11.2019 | [6. Funktionen](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/06_Funktionen.md#1)                                       |
|  2.12.2019 | [7. Zeiger](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/07_Zeiger.md#1)                                               |
|  9.12.2018 | [8. Input/Output](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/08_InputOutput.md#1)                                    |
|  16.12.2018 | [9. Dynamische Speicherverwaltung](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CCourse/master/09_DynamischeSpeicherverwaltung.md#1)  |

# ... und wozu brauche ich das?

                                 {{0-1}}
*******************************************************************************

**Antwort A:**
Das Studium vermittelt ein Weltbild und keine eng zugeschnitte Sicht.

**Antwort B:**
Die Fähigkeit in Algorithmen zu denken ist eine Grundlage wissenschaftlichen
Arbeitens.

**Antwort C:**
Am Ende steht Ihnen das Rüstzeug zur Verfügung kleine eingebettete C-Projekte
selbst anzugehen.

*******************************************************************************


                                 {{1-2}}
*******************************************************************************

**... zum Beispiel im Rahmen eines Arduino Projektes ...**

Mit einiger Erfahrung in C (und C++) lassen sich einfache Mess- und Regelungstechnikaufgaben
sehr einfach automatisieren. Ein Startpunkt dafür ist das Arduino Projekt, dass sowohl eine
entsprechende Hardware, wie auch eine Programmierumgebung bereitstellt.

```cpp        ArduinoHelloWorld.ino
void setup() {      // Konfiguration
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {       // Ausführung
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);                     
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);                     
}
```

**Ein bisschen realistischer bitte!**

... gut, dass ist noch nicht sonderlich beeindruckend. Vielleicht lässt folgende
Anwendung das Potential etwas deutlicher werden. Lassen Sie uns annehmen, wir
wollen die Lichtsitiation an einem bestimmten Punkt vermessen. Dazu verwenden
wir einen Sensor, der mit einem Controller verbunden ist und senden die
gesammelten Daten an einen Server. Dieser übernimmt die Aufbereitung und Visualisierung.

Forschungshypothese: Am Wochenende strahlt die Sonne heller.

![C logo](img/LightConditions.jpeg)<!--
style="width: 40%;" -->

<iframe width="450" height="260" style="border: 1px solid #cccccc;" src="https://thingspeak.com/channels/596617/charts/1?bgcolor=%23ffffff&color=%23d62020&days=1&dynamic=true&type=line"></iframe>

*******************************************************************************

# "C ist schwierig zu erlernen"

> Viele haben bei uns wegen dem Info-Grundlagenmodul gewechselt. Allerdings
> hängt das auch von dir und deinem Talent ab. Das Tempo ist rasant. Jede Art
> von Vorerfahrung hilft dir eigentlich sehr. Also wenn du noch Zeit hast vorm
> Studienbeginn, schnapp dir ein gutes Buch zur gelehrten Sprache, und fange
> schonmal bissl an kleine Sachen zu programmieren." _(Foreneintrag)_
>
> Ich habe es grade irgendwie selbst gelöst, aber keine Ahnung warum es
> funktioniert hat. _(Foreneintrag)_

Herausforderungen:

* Abstrakte Denkweise
* Penible Beachtung der Syntax
* Ungewohnte Arbeitsmittel

# Wie können Sie zum Gelingen der Veranstaltung beitragen?

* Stellen Sie Fragen, seinen Sie kommunikativ!
* Organisieren Sie sich in Arbeitsgruppen!
* Experimentieren Sie mit verschiedenen Entwicklungsumgebung um "Ihren Editor"
  zu finden
* Machen Sie Verbesserungsvorschläge für die Vorlesungsfolien!

![Atom IDE Screenshot](./img/screenShotAtom.png)<!-- width="100%" -->

Link auf den GitHub: https://github.com/liaScript/CCourse

# Und wenn Sie dann immer noch programmieren wollen ...

![WALL-E](./img/BAF_bots.png)<!--
style="width: 80%; display: block; margin-left: auto; margin-right: auto;" -->

# Autorenliste

Sebastian Zug, Galina Rudolf, Georg Jäger, André Dietrich, Tobias Bräuer
