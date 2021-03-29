# Allgemeines

## Neue View erstellen

1. Neue View und ViewModel erstellen
2. Im ViewModelLocator neues  ViewModel definieren und unten reinladen

`public DiscoPageViewModel DiscoPageVM => Services.GetService<DiscoPageViewModel>();`

`serviceCollection.AddSingleton<DiscoPageViewModel>();`

3. Im DataContext der neuen View die Definition einbinden 

 `DataContext="{Binding DiscoPageVM, Source={StaticResource Locator}}">`

Aus diesem DataContext kann man Bindings und Commands verwenden



## Content Control

- wird im MainWindow definiert, in der Zelle in die Pages geladen werden sollen

`<ContentControl Content="{Binding FrameNavigationService.Frame}"/>`



## Commands/ Bindings

- in ViewModel erstellte Commands benutzt man in den Views um Methoden auszuführen, z.B. bei ButtonPress

  `public RelayCommand RndColorCMD => new(() `

  `=>{OnPropertyChanged(nameof(RndColor));`

  `});`

- Werte werden zum Darstellen genutzt

  `public string RndColor`
          `{`
              `get => RndColorGenerator();`
          `}`

  `...`

  `Fill="{Binding RndColor}"`



## resx  ansprechen
- nachdem ein Wert in Resources.resx festgelegt wurde, kann man ihn ansprechen über  `Content="{x:Static p:Resources.Home}"`



##  OnPropertyChanged

- wird ausgeführt, wenn der Wert geupdated wurde, 
- `OnPropertyChanged(name)`

## SetProperty

- überprüft ob Property schon den gewünschten Wert hat, wen nicht ändert es und teilt den Listenern mit
- `SetProperty(ref _name,value)`
- _name ist das Property, muss Getter und Setter haben
- value ist der gewünschte Wert für _name



# Icon für Programm ändern

- Debug Modus beenden!
- Rechtsklick auf zweites von oben -> Application -> Icon and manifest
- .ico Datei verwenden