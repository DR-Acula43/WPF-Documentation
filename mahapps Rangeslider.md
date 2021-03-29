# mahapps Rangeslider

- Die Bindings LowerValue/ UpperValue erhalten den akutell gewählten Wert
- Mit `ChangeValueBy ="SmallChange"`wird eingestellt um wieviel der gesamte Bereich verschoben wird

  

```c#
 <mah:RangeSlider 
              Grid.Column="2"
            Grid.Row="1"
            Width="200"
           
                 Margin="4"
                 mah:SliderHelper.ChangeValueBy="SmallChange"
                 mah:SliderHelper.EnableMouseWheel="MouseHover"
                 AutoToolTipPlacement="TopLeft"
                 LargeChange="10"
                 LowerValue="{Binding LowerValue}"
                 Maximum="100"
                 Minimum="0"
                 Orientation="Horizontal"
                 SmallChange="1"
                 Style="{DynamicResource MahApps.Styles.RangeSlider.Win10}"
                 UpperValue="{Binding UpperValue}">
            <mah:RangeSlider.AutoToolTipRangeValuesTemplate>
                <DataTemplate DataType="mah:RangeSliderAutoTooltipValues">
                    <UniformGrid Columns="2" Rows="2">
                        <TextBlock HorizontalAlignment="Right" Text="From:" />
                        <TextBlock HorizontalAlignment="Right" Text="{Binding LowerValue, StringFormat='{}{0:N2}'}" />
                        <TextBlock HorizontalAlignment="Right" Text="To:" />
                        <TextBlock HorizontalAlignment="Right" Text="{Binding UpperValue, StringFormat='{}{0:N2}'}" />
                    </UniformGrid>
                </DataTemplate>
            </mah:RangeSlider.AutoToolTipRangeValuesTemplate>
        </mah:RangeSlider>
```

- `TickPlacement` gibt an ob Skala angezeigt werden soll, `TickFrequency`in welchem Abstand sie sind

- `IsSnapToTick=true`derRangeslider snapt nur an die Ticks, zB bei `TickFrequency=10`kann man nur 0,10,20,... auswählen

- `MinRange= 5`