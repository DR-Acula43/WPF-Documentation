# Message Senden

- Wird benutzt um z.B. zwischen Views und Window Daten auszutauschen
- Wenn ObservableObject eingebunden wird, kann die Klasse Messages sowohl senden als auch requesten, ObservableRecipient kann nur listenen
- Beispiel: In View ColorsPage drückt man einen Button, der dann eine Message mit einer Farbe sendet; in MainWindow ist ein Listener, der auf diese Nachricht wartet und dann den Hintergrund entsprechend setzt

###  Message erstellen & senden

1. Neue Message `Color.cs` erstellen, darin Klasse `ColorChanged` erstellt

2. Das ViewModel `ColorsPage.cs` muss `ObservableObject` einbinden `public class ColorsPageViewModel : ObservableObject    { }`

3. Das CMD `ChangeColorCmd` sendet eine Message des Typs `SolidColorBrush` los, erstmal nicht an einen bestimmten Ort

   `public RelayCommand<System.Windows.Media.SolidColorBrush> ChangeColorCmd => new(`

   ​		`color =>{`

   ​			`WeakReferenceMessenger.Default.Send(new Messages.ColorChanged(color));`

   ​	`			},`

   ​	`color => true`

   `);`

4.  Der Button bindet den CMD, sodass dann die Message gesendet wird (Background wird per Path als CommandParameter mitgesendet) `<Button x:Name="B00" Background="red" Command="{Binding ChangeColorCmd}" CommandParameter="{Binding ElementName=B00, Path=Background}"/>`

### Message empfangen 

5. MainWindow listened auf die Nachricht von `ColorChanged` und muss `ObservableRecipient` einbinden `public class MainWindowViewModel : ObservableRecipient { }`

6.  Am Besten Dekonstruktor erstellen und IsActive = true;

   `~MainWindowViewModel(){IsActive = false`;}

7. MainWindow erhält die Farbe und speichert sie in dem Binding BackgroundColor 

   `protected override void OnActivated()`
           {
               `WeakReferenceMessenger.Default.Register<Messages.ColorChanged>(this, (r, m) =>`
               {
                   `BackgroundColor = m.Value;`
               });
               `WeakReferenceMessenger.Default.Register<Messages.ColorStateChannelRequest>(this, (r, m) =>`
               {
                   `m.Reply(BackgroundColor);`
               `});`
               `base.OnActivated();`
           }

   ...

   `private SolidColorBrush _backgroundColor = new SolidColorBrush(Colors.Blue);`
           `public SolidColorBrush BackgroundColor` 
           {
               `get => _backgroundColor;`
               `set => SetProperty(ref _backgroundColor, value);`
           }

8. Dieses Binding wird in MainWindow.xaml als Hintergrundfarbe benutzt 

   `<Grid Background="{Binding BackgroundColor}">`

9. 

