# Lokalisierung dynamisch

- gute Anleitung für eine Methode zur dynamischen Lokalisierung

  -> [Dynamic Localization In WPF (c-sharpcorner.com)](https://www.c-sharpcorner.com/article/dynamic-localization-in-wpf/)

- jede Seite hat hier ihre eigene Resourcendatei (übersichtlicher pro Datei, jedoch mehr Resourcendateien)

- Beachten: 

  - bei jeder neu hinzugefügten Resourcendatei Properties -> Build = Content & Copy = If Newer

## Implementation

### Cultures wechseln mit Buttons

- Nachteil ist, dass für jede Culture eine eigene Methode geschrieben werden muss
- Code Behind

```c#
 private void ClickEn(object sender, RoutedEventArgs e)
        {
            LocUtil.SwitchLanguage(this, "en-US");
        }
```

