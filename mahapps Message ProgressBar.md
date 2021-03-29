# Show Message Dialog

- Zeigt eine Nachricht im Windows Design an, mit einem Button der Betätigt werden muss, damit Sie weggeht
- `<Button Content="Klick"  Click="OnButtonClick"/>`
- `private async void OnButtonClick(object sender, RoutedEventArgs e)
          {
              await this.ShowMessageAsync("This is the title", "Some message");
          }`
- ist im Code-Behind zu implementieren
- (Nur in Window-Klasse! Mit MEssages machen?)



# Show Progress Bar Dialog

`var controller = await this.ShowProgressAsync("Please wait...", "Progress message");
            controller.SetProgress(0.33);
            controller.SetProgress(1.0);
            controller.SetCancelable(true);`

- Gibt noch mehr Methoden, wie zB ISCancelled