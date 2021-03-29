# Converter

### Converter anwenden

- entsteht wenn man Klasse/Typ schreibt, der `IValueConverter`implementiert

- Beispiel: Man möchte einen Button mit Visibilty ausblenden, wenn ein Wert false ist

  -> geht nicht, weil Visibility nimmt ja nicht true/false sonder Collapsed/Visible/Hidden

- in App.xaml im ResourceDictionary ` <c:PrioConverter x:Key="PrioConverter"/>`hinzufügen

  

```c#
<mah:ProgressRing  
                          Grid.Column="1"
                          Grid.Row="2"
                     Visibility="{Binding IsLoading, Converter={StaticResource BooleanToVisibilityConverter}}"
                          />
```

### Converter erstellen

- BoolToVisibilityConverter

  

```c#
using System;
using System.Globalization;
using System.Windows;
using System.Windows.Data;

namespace HausUndKlo.Converters
{
    public class BoolToVisibility : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            if (value is bool)
            {
                if ((bool)value)
                {
                    return Visibility.Visible;
                }
                return Visibility.Collapsed;
            }
            throw new Exception("value must be of type boolean");
        }

        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            if (value is Visibility)
            {
                if ((Visibility)value == Visibility.Visible)
                {
                    return true;
                }
                return false;
            }
            throw new Exception("value must be of type visibility");
        }
    }
}
```

