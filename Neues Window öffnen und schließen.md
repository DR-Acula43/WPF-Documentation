# Neues Window öffnen und schließen

### Window öffnen

- Button auf einer Seite Settings öffnet ein neues Window

- Das (Metro-)Window Subwindow.xaml erstellen und `using MahApps.Metro.Controls;`im Code Behind

- in Settings.xaml.cs die Methode erstellen:

- `private void OpenRestartPrompt(object sender, RoutedEventArgs e)
          {
              SubWindow subWindow = new SubWindow();
              subWindow.Show();
          }`
      
- subWindow.ShowDialog(); wenn Nutzer nicht auf andere Fenster zugreifen darf, solange dieses noch offen ist

- Hinweis: Auf die Methode zugreifen mit Click="OpenRestartPrompt" als Property des Buttons

     

### Window schließen

- Ein Button wird das eben neu geöffnete Window wieder schließen

- In der View des neuen Fensters ist der Button definiert

- Hinweis: behaviors einbinden

  

```c#
 xmlns:i="http://schemas.microsoft.com/xaml/behaviors" 
...
<Button Content="Ok" Width="60" Height="30" Grid.Row="1">
            <i:Interaction.Triggers>
                <i:EventTrigger EventName="Click">
                    <i:CallMethodAction MethodName="Close"
                           TargetObject="{Binding RelativeSource={RelativeSource  Mode=FindAncestor,   AncestorType=Window}}" />
                </i:EventTrigger>
            </i:Interaction.Triggers>
        </Button>
```

