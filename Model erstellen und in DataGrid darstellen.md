# Model erstellen und in DataGrid darstellen

### Model erstellen

- Models -> Add -> new Model
- Die obige Klasse ist Contacts, die untere Contact
- In unterer Getter und Setter für Attribute erstellen (Name, Adresse, IsSet. etc...)

### Im ViewModel

- Eine Liste des generischen Typs Contacts erstellen (using XXX.Models;) und Getter/Setter deklarieren

  ​    `    public Contacts ContactList { get; set; } = new Contacts();`

- Gewünschte Nutzer hinzufügen `ContactList.Add(new Contact(){Name="Simon"});`

- Beachten!!! Konstruktor Singular verwenden

- Hinweis: Möchte man SelectedItem verwenden, um die Daten aus der DataGrid separat anzuzeigen, muss im Setter von SelectedContact OnPropertyChanged für jedes Property aufgerufen werden, um diesen Feldern auch mitzuteilen, dass sich etwas geändert hat!

-  `private Contact _selectedContact;`
          `public Contact SelectedContact`
          `{`
              `get => _selectedContact;`
              `set {` 
                  `SetProperty(ref _selectedContact, value);`
                  `OnPropertyChanged(nameof(SelectedNachName));`
                  `OnPropertyChanged(nameof(SelectedVorName));`
                  `OnPropertyChanged(nameof(SelectedAdresse));`
                  `OnPropertyChanged(nameof(SelectedEMail));`

  `}`

  `}`

### In der View

- über das im VM erstellte Binding kann man die Liste als Itemssource für eine DataGrid verwenden

  '  <DataGrid ItemsSource="{Binding UserList, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged, NotifyOnSourceUpdated=True}" 
                    AutoGenerateColumns="False" 
                    SelectionMode="Single">'

- In den einzelnen Spalten wählt man über Bindings, welche Attribute dargestellt werden

<DataGrid.Columns>
                    <DataGridTextColumn Header="{x:Static prop:Resources.surname}" Binding="{Binding Nachname}" IsReadOnly="True"/>
                               </DataGrid.Columns>