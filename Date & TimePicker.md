# Date & TimePicker

### DatePicker

- `<DatePicker Grid.Row="0" Grid.Column="3" SelectedDate="{Binding Date2}" DisplayDate="01-03-2021" Height="30" Width="25"/>`   
- Zeigt einen Kalender an, bei dem durch Anklicken eines Datums dieses an das Binding Date2 gegeben wird
- Date2 muss vom Typ DateTime sein, liefert sowohl Datum als auch eine Uhrzeit
- Man kann (theoretisch) mit Date2.Date nur das Datum/Jahr usw. rausfiltern
- Hinweis: .Date und DisplayDate haben bei mir nicht funktioniert
- `get => _date2.ToString().Remove(10,_date2.ToString().Length-10);`
- Um nur das Datum zu erhalten (ohne Zeitangabe) habe ich es in einen String umgewandelt und dann alle unnötigen removt (01.34.6789)

### TimePicker

- ​        `<mah:TimePicker Grid.Row="1" Grid.Column="3" Height="30" Width="25" SelectedDateTime="{Binding Time2}"/>` 
- ist von mahapps
- funktioniert wie DatePicker
- mit Time2.TimeOfDay kann man die Uhrzeit aus der DateTime filtern (funktioniert auch in XAML)