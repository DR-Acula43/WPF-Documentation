# Global Styles anwenden

- in App.xaml

  

```
  <ResourceDictionary>
            <Style TargetType="Label">               
                <Setter Property="FontSize" Value="20"/>
            </Style>
            <Style TargetType="Button">
                <Setter Property="Background" Value="LightGray"/>
                <Setter Property="FontStyle" Value="Italic"/>                
            </Style>
            ...
            
 </ResourceDictionary>
```

- setzt man den Style eines Objekt direkt, überschreibt es das aus dem ResourceDictionary