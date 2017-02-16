# Programmierregeln

Die folgenden Vorgehensweisen steigern die Lesbarkeit, Wartbarkeit oder Flexibilität von Programmcode, oder sie steigern die Eingriffsmöglichkeiten des Compilers im Fall von Flüchtigkeitsfehlern. **Sie sollten daher von neu aufgestellten Programmierregeln nicht eingeschränkt werden.** Es sollte also möglich sein, die folgenden Programmierstile zu nutzen, ohne damit gegen aufgestellte Regeln verstoßen zu müssen.

## Komponentenbasierte Strukturierung des Projekts

Eigenschaften einer Komponente:

 * unabhängig von der umgebenden Ordnerstruktur und von den umgebenden Dateien
 * einmalig konfigurierbar (bei der Instanzierung)
 * funktionstüchtig auch ohne aufwändige Konfiguration (Verfügbarkeit brauchbarer Default-Werte)
 
Die Unabhängigkeit von der umgebenden Ordnerstruktur ist der wichtigste Punkt, da sie die Flexibilität der Komponente am stärksten beeinflussen kann. Idealerweise sollte die Komponente in ein beliebiges Verzeichnis verschoben werden können und dort auf Anhieb funktionieren, wenn die benötigten Abhängigkeiten (Pakete/Referenzen) installiert/konfiguriert sind.

## Separation of Concerns

Kurz zusammengefasst (passend zur vielgelobten Unix-Philosophie):

**"Write independent functions/methods/modules that do one thing and do it well"**

Vorteile:

 * Testbarkeit auf Anhieb, ohne umschreiben zu müssen (Unit-Tests)
 * mehr Flexibilität
 * mehr Verständlichkeit
 
Daher soll es erlaubt sein, ...
 * kurze Funktionen/Methoden zu schreiben
 * kurze Dateien zu schreiben

## Immutability

Die Unterscheidung zwischen zur Laufzeit unveränderbaren und veränderbaren Objekten erhöht die Verständlichkeit von Programmcode.

Vorteile:
 * deutlich schnelleres Debugging
 * weniger Denkfehler
 * weniger Flüchtigkeitsfehler durch bessere Compiler-Unterstützung

Durch die Programmiersprache C# **bereits erzwungene Immutability**, die nur mittels Reflection umgangen werden kann:
 * Klassen
 * Funktionen/Methoden

Durch den Entwickler wählbare Immutability:
 * Read-only/Get-only-Properties
 * Konstanten mit Function/Method-Scope (lokale Konstanten)

Immutability ist kein Alles-oder-Nichts-Prinzip: je weniger Immutability, desto schlechter; je mehr Immutability, desto besser.

Erklärung: Jeder explizit fixierte Wert verringert die Freiheitsgrade eines instanzierten Objekts um genau einen Freiheitsgrad. Damit ist es berechenbarer (für Menschen schneller durchschaubar).

100% Immutability zu erreichen ist unsinnig (da unmöglich), 70% Immutability erfahrungsgemäß schon ein guter Wert.

## Redundanz in der statischen Typisierung

**Beispiel**

Wenn Folgendes genehmigt ist ...
```typescript
const url = page.getUrl();
```

... soll Folgendes trotzdem nicht verboten sein:
```typescript
const url: string = page.getUrl();
```

Da es die Fehlererkennungsmöglichkeiten des Compilers erweitert und damit den Code robuster macht (und darüber hinaus für Menschen lesbarer).

## Namensgebung

Die folgenden Namensgebungsregeln orientieren sich an der gängigen Praxis in den meisten Programmiersprachen:
 * Klassen/Interfaces: Nomen (großer Anfangsbuchstabe)
 * Funktionen/Methoden: Verben+Nomen
 * Konstanten/Variable/Properties (keine Booleans): Nomen (TypeScript: kleiner Anfangsbuchstabe)
 * Konstanten/Variable (Booleans): Adjektive oder Verben (Partizip Präsens/Perfekt)

Damit erkennt man auf den ersten Blick am Variablennamen, dass in TypeScript ...
 * Adjektive und Partizip-Verben mit Sicherheit Booleans sind
 * Nomen mit kleinem Anfangsbuchstaben mit Sicherheit Konstanten, Variable oder Properties sind
 * Identifiers mit Verben im Namen mit Sicherheit Funktionen oder Methoden bezeichnen
 * Identifiers, die Nomen mit großem Anfangsbuchstaben sind, sehr wahrscheinlich Klassen oder Interfaces benennen
