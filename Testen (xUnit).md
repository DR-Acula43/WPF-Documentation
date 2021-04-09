# Testen

- Da bei MVVM das ViewModel unabhängig von dem UI ist, kann man gut Unit Tests benutzen
- Unit-Tests sollen F.I.R.S.T. erfüllen:
  - Fast
  - Independent (Tests untereinander unabhängig)
  - Repeatable (wiederholbar in beliebiger Umgebung, zB kein Zugang zu Internet notwendig)
  - Self-Validating (Test entweder grün der rot, muss man z.B. überprüfen ob Datei auch geschrieben wurde, verletzt es das S.)
  - Timely (vor oder mit dem Code schreiben)
- Vorteile von Tests:
  - Beim Schreiben der Tests denkt man schon über die Implementierung nach
  - Gute Tests geben gute Dokumentation



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