# Wert aus TextBox lesen

- In diesem Beispiel werde ich eine TexBox erstellen und mithilfe eines Bindings den Wert auslesen. Zur Überprüfung wird der Wert gleich in ein Label geschrieben
- <TextBox Text="{Binding Subject}"/>

  -> der ausgelesene Wert wird in Subject gespeichert
- <Label Content="{Binding Subject}" />

  -> das gleiche Binding wird zur Überprüfung zum Darstellen verwendet
- Hinweis: im Setter von Subject mit OnPropertyChanged(nameof(Subject)) arbeiten, so dass die Änderung gleich sichtbar wird