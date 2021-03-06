<!--

author:   Sebastian Zug & André Dietrich & Galina Rudolf
email:    sebastian.zug@informatik.tu-freiberg.de & andre.dietrich@ovgu.de & Galina.Rudolf@informatik.tu-freiberg.de
version:  0.0.1
language: de
narrator: Deutsch Female

import: https://raw.githubusercontent.com/liaScript/rextester_template/master/README.md
-->

# Vorlesung I - Einführung

Hier geht es zur interaktiven Version des Kurses [LiaScript](https://liascript.github.io/course/?https://raw.githubusercontent.com/SebastianZug/CCourse/master/01_Einfuehrung.md#1)!

**Fragen an die heutige Veranstaltung ...**

* Wie wird ein textuelles Programm in einen ausführbaren Code transformiert?
* Was bedeutet der Begriff Hochsprache, was verbirgt ist ein Assembler?
* Woraus ergibt sich die Aktualität der Sprache C?
* Welche Eigenschaften grenzt C von anderen Programmiersprachen ab?
* Welche Aufgabe hat ein Compiler?
* Wordurch definieren sich verschiedene "Geschmacksrichtungen" im
  Entwicklungsprozess?

## 1. Grundlegendes

Programme sind Anweisungslisten, die vom Menschen erdacht, auf einem Rechner zur
Ausführung kommen. Eine zentrale Hürde ist dabei die Kluft zwischen menschlicher
Vorstellungskraft und Logik, die **implizite Annahmen und Erfahrungen**
einschließt und der **"stupiden" Abarbeitung von Befehlsfolgen** in einem
Rechner.

Programmiersprachen bemühen sich diese Lücke zu schließen und werden dabei von
einer Vielzahl von Tools begleitet, diesen **Transformationsprozess**
unterstützen sollen.

Um das Verständnis für diesen Vorgang zu entwickeln werden zunächst die Vorgänge
in einem Rechner bei der Abarbeitung von Programmen beleuchtet, um dann die
Realisierung eines Programmes mit C zu adressieren.

![instruction-set](./img/Programmiersprache_Umfeld.png)<!-- width="100%" -->

Quelle: [Programmiervorgang und Begriffe(Autor VÖRBY)](https://commons.wikimedia.org/wiki/File:Programmiersprache_Umfeld.png)


### Wie arbeitet ein Rechner eigentlich?

Beispiel: Intel 4004-Architektur (1971)

![intel](https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/4004_arch.svg/1190px-4004_arch.svg.png)<!-- style="width: 80%; display: block; margin-left: auto; margin-right: auto;" -->

Quelle: [Intel 4004 (Autor Appaloosa)](https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/4004_arch.svg/1190px-4004_arch.svg.png)


### Was heißt das "Maschinensprache"?

Jeder Rechner hat einen spezifischen Satz von Befehlen, die durch "0" und "1"
ausgedrückt werden, die er überhaupt abarbeiten kann.

Speicherauszug den Intel 4004:


         {{0-1}}
| Adresse | Speicherinhalt |
|:--------|:---------------|
| 0010    | 1101 0101      |
| 0012    | 1111 0010      |


                         {{1}}
| Adresse | Speicherinhalt | OpCode     | Mnemonik  |
|:--------|:---------------|:-----------|:----------|
| 0010    | 1101 0101      | 1101 DDDD  | LD $5     |
| 0012    | 1111 0010      | 1111 0010  | IAC       |


Unterstützung für die Interpretation aus dem Nutzerhandbuch, dass das Instruction
set beschreibt:

![instruction-set](./img/4004_Instruction_set.png)<!-- width="100%" -->

Quelle: [Intel 4004 Assembler](http://e4004.szyc.org/asm.html)

### Aber möchte man so umfangreiche Programme schreiben?

**Vorteil:** ggf. sehr effizienter Code (Größe, Ausführungsdauer), der gut auf die
Hardware abgestimmt ist

**Nachteile:**

* systemspezifische Realisierung
* geringer Abstraktionsgrad, bereits einfache Konstrukte benötigen viele Codezeilen
* weitgehende semantische Analysen möglich

**Beispiel**

```asm @output
 Assembler Code    |  Fortran
                   |
 .START ST         |  A:=2;
 ST: MOV R1, #2    |  FOR I:=1 TO 20 LOOP
     MOV R2, #1    |      A:=A*I;
 M1: CMP R2, #20   |  END LOOP;
     BGT M2        |  PRINT(A);
     MUL R1, R2    |
     INI R2        |
     JMP M1        |
 M2: JSR PRINT     |
 .END              |
```

                                   {{1}}
> Eine höhere Programmiersprache ist eine Programmiersprache zur Abfassung eines
> Computerprogramms, die in **Abstraktion und Komplexität** von der Ebene der
> Maschinensprachen deutlich entfernt ist. Die Befehle müssen durch
> **Interpreter oder Compiler** in Maschinensprache übersetzt werden.

### Compiliervorgang

> Ein **Compiler** (auch Kompiler; von englisch für zusammentragen bzw.
> lateinisch compilare ‚aufhäufen‘) ist ein Computerprogramm, das Quellcodes
> einer bestimmten Programmiersprache in eine Form übersetzt, die von einem
> Computer (direkter) ausgeführt werden kann.


Stufen des Compile-Vorganges:

![instruction-set](./img/compilerElements.png)<!-- width="80%" -->

Quelle: [Stufen der Compilierung](https://medium.com/@vietkieutie/what-happens-when-you-type-gcc-main-c-2a136896ade3)

## 2. Warum also C?

Warum gibt es nicht eine höhere Programmiersprache, die für alle Anwendungen
gleichermaßen herangezogen werden kann?

* unterschiedliche Plattformen (Betriebssystem, Rechnerarchitektur)

  *Windows-Laptop vs. Steuergerät vs. Grafikkarte*

* unterschiedliche Anwendungen

  *Website vs. PKW Spurerkennung vs. Datenbankabfrage*

* unterschiedliche Randbedingungen

  *Echtzeitfähigkeit, Sicherheitsanforderungen*


Und wie finde ich die Sprache, die für mein Problem geeignet ist?

* Analyse der Anforderungen
* Analyse der Fähigkeiten einzelner Sprachen
* Analyse der Features möglicher Bibliotheken oder Frameworks
* Analyse des Einarbeitungsaufwandes
* (Kosten für die Tool-Chain)

[Heise online: Die passende Programmiersprache finden](https://www.heise.de/ct/ausgabe/2015-18-Die-passende-Programmiersprache-finden-2767703.html)

### Relevanz von C im Vergleich mit anderen Programiersprachen

Relevanz laut Tiobe Index (Oktober 2018)

![TIOBEindex](./img/tiobe.jpeg)<!-- style="width: 80%; display: block; margin-left: auto; margin-right: auto;" -->

Quelle: [https://www.informatik-aktuell.de](https://www.informatik-aktuell.de/aktuelle-meldungen/2018/juli/ranking-der-programmiersprachen-java-wieder-ganz-vorne.html)


### Heutige Anwendung

* Eingebettete Systeme -> Siehe Beispiel
* Programmierung von Betriebssystemen
* Anwendungsentwicklung -> Java Virtual Maschine (JVM)

![instruction-set](./img/InterpreterVSCompiler.jpg)<!-- style="width: 70%; display: block; margin-left: auto; margin-right: auto" -->

Quelle: [https://www.computerlanguage.com (Alan Freedman, Irma Morrison)](https://www.computerlanguage.com/results.php?definition=interpreter)

### Historische Einordnung

Zielrichtung ... Entwicklung eines Betriebssystems in den
*AT&T Bell Laboratories* Anfang 1970

![instruction-set](./img/Ken_Thompson_and_Dennis_Ritchie.jpg)<!-- width="300px" -->

[Ken Thompson](https://de.wikipedia.org/wiki/Ken_Thompson) und [Dennis Ritchie](https://de.wikipedia.org/wiki/Dennis_Ritchie)

Quelle: [http://www.catb.org/~esr/jargon/html/U/Unix.html](http://www.catb.org/~esr/jargon/html/U/Unix.html)

![instruction-set](./img/Brian_Kernighan.jpg)<!-- width="300px" -->

[Brian Kernighan](https://de.wikipedia.org/wiki/Brian_Kernighan)

Quelle: [http://www.catb.org/~esr/jargon/html/U/Unix.html](http://www.catb.org/~esr/jargon/html/U/Unix.html)

| Version      | Spezifikation                                                                                 |
|:-------------|:----------------------------------------------------------------------------------------------|
| K&R C        | Definition über das Buch "The C Programming Language"                                         |
| ANSI C (C89) | Standard des American National Standards Institute (ANSI)                                     |
| C99          | Übernahme von Features aus C++, Erweiterung Standardbibliothek, Ergänzung Präprozessor Makros |
| C11          |   bessere Kompatibilität mit C++, einige neue Features       |
| C18          | entspricht weitgehend C11 mit der Ausnahme von Fehlerkorrekturen    |

Die Veranstaltung baut auf dem C11 (ISO/IEC 9899:2011) Standard auf.

``` cpp
#if defined(__STDC_VERSION__) && __STDC_VERSION__ >= 201112L
 // C11-kompatibler Quellcode.
#endif
```

### Eigenschaften von C

* Adressiert Hochsprachenaspekte und Hardwarenähe -> Hohe Geschwindigkeit bei
  geringer Programmgröße
* Imperative Programmiersprache

                                 {{1}}
  > **imperative (befehlsorientierte) Programmiersprachen**: Ein Programm
  > besteht aus einer Folge von Befehlen an den Computer. Das Programm
  > beschreibt den Lösungsweg für ein Problem (C, Python, Java, LabView,
  > Matlab, ...).
  >
  > **deklarative Programiersprachen**: Ein Programm beschreibt die
  > allgemeinen Eigenschaften von Objekten und ihre Beziehungen
  > untereinander. Das Programm beschreibt zunächst nur das Wissen zur Lösung
  > des Problems (Prolog, Haskal, SQL, ...).


* Wenige Schlüsselwörter als Sprachumfang

                                  {{2}}
  > **Schlüsselwort** Reserviertes Wort, das der Compiler verwendet, um ein
  > Programm zu parsen (z.B. if, def oder while). Schlüsselwörter dürfen nicht
  > als Name für eine Variable gewählt werden

* Große Mächtigkeit

                                  {{3}}
  > Je "höher" und komfortabler die Sprache, desto mehr ist der Programmierer
  > daran gebunden, die in ihr vorgesehenen Wege zu beschreiten.

## 3. Erstes C Programm

![instruction-set](./img/helloWorldFromRitchie.png)<!-- width="90%" -->

Quelle: [Brian_Kernighan, Programming in C: A Tutorial  1974](http://www.lysator.liu.se/c/bwk-tutor.html#simple-c)

### "Hello World"

```cpp                     smallestCProgram.c
int main() {   // <- Öffnende Klammer eines Blockes
	return 0;    // <- Befehl endet mit Semikolon
}              // <- Schließende Klammer eines Blockes
```
@Rextester.C

Führen Sie das Programm durch Klicken des Buttons aus. Überrascht Sie die Ausgabe?

```cpp                     HelloWorld.c
// That's my first C program
// Karl Klammer, Oct. 2018

#include<stdio.h>

int main(void) {     // alternativ "int main()"
	printf("Hello World");
	return 0;
}
```
@Rextester.C

| Zeile | Bedeutung                                                                                   |
|:------|:--------------------------------------------------------------------------------------------|
| 1 - 2 | Kommentar (wird vom Präprozessor entfernt)                                                  |
| 4     | Voraussetzung für das Einbinden von Befehlen der Standardbibliothek hier `printf()`         |
| 6     | Einsprungstelle für den Beginn des Programmes                                               |
| 6 - 9 | Ausführungsblock der `main`-Funktion                                                        |
| 7     | Anwendung einer Funktion ... `name(Parameterliste)` ... hier zur Ausgabe auf dem Bildschirm |
| 8     | Definition eines Rückgabewertes für das Betriebssystem                                      |


### Ein Wort zu den Formalien

```cpp                     HelloWorld.c
// Karl Klammer
// Print Hello World drei mal

#include <stdio.h>

int main() {
  int zahl;
  for (zahl=0; zahl<3;  zahl++){
	    printf("Hello World! ");
  }
	return 0;
}
```
@Rextester.C


```cpp                     BadHelloWorld.c
#include <stdio.h>
int main() {int zahl; for (zahl=0; zahl<3;  zahl++){ printf("Hello World! ");} return 0;}
```
@Rextester.C

                                  {{1}}
* Das *systematische Einrücken* verbessert die Lesbarkeit und senkt damit die
  Fehleranfälligkeit Ihres Codes!
* Wählen sie *selbsterklärende Variablen- und Funktionsnamen*!
* Nutzen Sie ein *Versionsmanagmentsystem*, wenn Sie ihren Code entwickeln!
* Kommentieren Sie Ihr Vorgehen trotz "Good code is self-documenting"

### Gute Kommentare

*1. Kommentare als Pseudocode*

```cpp
/* loop backwards through all elements returned by the server
(they should be processed chronologically)*/
for (i = (numElementsReturned - 1); i >= 0; i--){
    /* process each element's data */
    updatePattern(i, returnedElements[i]);
}
```

*2. Kommentare zur Datei*

```cpp
// This is the mars rover control application
//
// Karl Klammer, Oct. 2018
// Version 109.1.12

int main(){...}
```

*3. Beschreibung eines Algorithmus*

```cpp
/* Function:  approx_pi
 * --------------------
 * computes an approximation of pi using:
 *    pi/6 = 1/2 + (1/2 x 3/4) 1/5 (1/2)^3  + (1/2 x 3/4 x 5/6) 1/7 (1/2)^5 +
 *
 *  n: number of terms in the series to sum
 *
 *  returns: the approximate value of pi obtained by suming the first n terms
 *           in the above series
 *           returns zero on error (if n is non-positive)
 */

 double approx_pi(int n);
```

In realen Projekten werden Sie für diese Aufgaben Dokumentationstools verwenden,
die die Generierung von Webseite, Handbüchern auf der Basis eigener
Schlüsselworte in den Kommentaren unterstützen ->
[doxygen](http://fnch.users.sourceforge.net/doxygen_c.html).

*4. Debugging*

```cpp
int main(){
  ...
  preProcessedData = filter1(rawData);
  // printf('Filter1 finished ... \n');
  // printf('Output %d \n', preProcessedData);
  result=complexCalculation(preProcessedData);
  ...
}
```

### Schlechte Kommentare

*1. Überkommentierung von Code*

```cpp
x = x + 1;  /* increment the value of x */
printf("Hello World\n"); // displays Hello world
```

"... over-commenting your code can be as bad as under-commenting it"

Quelle: [C Code Style Guidelines](https://www.cs.swarthmore.edu/~newhall/unixhelp/c_codestyle.html)

*2. "Merkwürdige Kommentare"*

``` JavaScript
//When I wrote this, only God and I understood what I was doing
//Now, God only knows

// sometimes I believe compiler ignores all my comments

// Magic. Do not touch.

// I am not responsible of this code.

try {

} catch(e) {

} finally { // should never happen }

```

[Sammlung von Kommentaren](https://fuzzzyblog.blogspot.com/2014/09/40-most-funny-code-comments.html)


### Was tun, wenn es schief geht?

```cpp                     ErroneousHelloWorld.c
#include<stdio.h>

int main() {
  for (zahl=0; zahl<3;  zahl++){
	    printf("Hello World ! ")
  }
	return 0;
}
```
@Rextester.C

Methodisches Vorgehen:

* ** RUHE BEWAHREN **
* Lesen der Fehlermeldung
* Verstehen der Fehlermeldung / Aufstellen von Hypothesen
* Systematische Evaluation der Thesen
* Seien Sie im Austausch mit anderen (Kommilitonen, Forenbesucher, usw.) konkret

### Compilermessages

**Beispiel 1**

```cpp                     Error.c
#include <stdio.h>

int mani() {
    printf("Hello World");
    return 0;
}
```
@Rextester.C

**Beispiel 2**

```cpp                     Error.c
#include <stdio.h>

int main()
    printf("Hello World");
    return 0;
}
```
@Rextester.C

Dabei hängen die Ausgaben entscheidend vom verwendeten Compiler ab. Der Fehler bleibt aber der gleiche :-)

```cpp                     Error.c
#include <stdio.h>

int main()
    printf("Hello World");
    return 0;
}
```
@Rextester.C_clang

**ABER ...**

![instruction-set](./img/AuftretenCompilerFehler.png)<!-- style="width: 90%; display: block; margin-left: auto; margin-right: auto;" -->

Übersicht zu Compilernachrichten und Interpretationshilfe unter
http://aop.cs.cornell.edu/errors/index.html


### Und wenn das Kompilieren gut geht?

... dann bedeutet es noch immer nicht, dass Ihr Programm wie erwartet
funktioniert.

```cpp                     ErroneousHelloWorld.c
#include <stdio.h>

int main() {
  char zahl;
  for (zahl=250; zahl<256; zahl++){
	    printf("Hello World !");
  }
	return 0;
}
```
@Rextester.C


## 4. Werkzeuge

**Vim oder Eclipse?**

In the end, you want something that's going to make you the most productive.
Whether that's Notepad or Vim or Sublime or something else is up to the user and
the tasks required at the time. \[Forenbeitrag\]

![instruction-set](./img/VisualStudio.jpg)<!-- style="width: 90%; display: block; margin-left: auto; margin-right: auto;" -->

> Eine integrierte Entwicklungsumgebung (Abkürzung IDE, aus dem Englischen
> "integrated development environment") ist eine Sammlung von
> Computerprogrammen, mit denen die Aufgaben der Softwareentwicklung möglichst
> ohne Medienbrüche bearbeitet werden können.


### Arbeitsumgebung

* Arbeiten mit der LiaScript-Umgebung
* Online-Compiler und Ausführungsumgebungen für C

     https://www.onlinegdb.com/online_c_compiler

     https://www.learn-c.org/en/Welcome

* Lokale Tool-Chain auf dem eigenen Rechner (Pelles C)

![instruction-set](./img/pelles.png)<!-- style="width: 90%; display: block; margin-left: auto; margin-right: auto;" -->



## Ausblick

```cpp                     GoodBye.c
#include <stdio.h>

int main() {
  printf("... bis zum nächsten Mal!");
	return 0;
}
```
@Rextester.C
