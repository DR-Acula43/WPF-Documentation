# INotifyPropertyChanged 

- In der ViewModel das Interface implementieren

-  ` public class CalcPageViewModel : ObservableObject, INotifyPropertyChanged
      { ...  } `
      
- das Binding definieren

- `private string _showValue = "0";
          public string ShowValue
          {
              get => _showValue;
              set => SetProperty(ref _showValue, value);
          }`
      
- -------------------------------------------

- Wenn der Wert geändert wird, die Methode `OnPropertyChanged(nameof()) mit dem Binding, NICHT dem private aufrufen!

- ` _showValue = _showValue + number;
                       OnPropertyChanged(nameof(ShowValue));`

