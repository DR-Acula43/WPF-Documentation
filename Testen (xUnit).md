# Testen

- Da bei MVVM das ViewModel unabhängig von dem UI ist, kann man gut Unit Tests benutzen
- Unit-Tests sollen F.I.R.S.T. erfüllen:
  - Fast
  - Independent (Tests untereinander unabhängig)
  - Repeatable (wiederholbar in beliebiger Umgebung, zB kein Zugang zu Internet notwendig)
  - Self-Validating (Test entweder grün der rot, muss man z.B. überprüfen ob Datei auch geschrieben wurde, verletzt es das S.)
  - Timely (vor oder mit dem Code schreiben)
- ViewModels werden Testbar, indem Abhängigkeit abstrahiert werden
- Vorteile von Tests:
  - Beim Schreiben der Tests denkt man schon über die Implementierung nach
  - Gute Tests geben gute Dokumentation

### Beim Testen beachten

- Vorteil ist nicht direkt zu spüren, nur indirekt

- Konstruktiv: Fehler vermeiden, durch Auswählen richtiger Tools/ Prozesse, Kommunikation

- Analytisch: Fehler finden, Testen 

- Systematisch Testen:

  - Mithilfe von Äquivalenzklassen (siehe unten) geeignete Stichproben wählen
  - Randbedingungen erfassen (z.B. Umgebung, interagiert es mit anderen Klassen)
  - Ergebnisse dokumentieren

- Äquivalenzklassen:

  - Annehmen, dass sich ähnliche Eingaben und Zustände ähnlich verhalten

  - Beispiel Blitzer:

  - ÄK 1: Erlaubtes Tempo: 1 - 50 km/h

  - Äk 2: Toleranz: 51-55 km/h

  - Äk 3: Überschreitung: >55 km/h

  - ungültige Äk: <= 0 km/h

  - -> jeder Wert in einer ÄK sollte sich gleich verhalten

  - -> bei Randwertanalyse wählt man Anfang und Ende einer einer ÄK anstatt beliebigen Wert

    

### Tests implementieren

- die NuGet-Packages *xUnit* und *xUnit.runner.visualstudio* installieren

- über Tab *Test -> TestExplorer* öffnen

- auf *Projektmappe Rechtsklick -> Hinzufügen ->Neues Projekt -> xUnit Vorlage* auswählen

- Bei dem *neuen Projekt Rechtsklick auf Verweise/Abhängigkeiten -> Verweis hinzufügen -> Haken bei richtigem Projekt setzen -> OK*

- ```c#
  [Fact]	//zeigt, dass diese Methode ein Test ist
          public void Addition()
          {
              Assert.Equal(2, 1 + 1);
          }
  ```

  

- Im TestExplorer auf grünen Pfeil (Run All)