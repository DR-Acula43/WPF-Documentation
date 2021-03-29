# Elemente für Einstellungs-Seite

### Toggle Switch

`<mah:ToggleSwitch Header="{x:Static prop:Resources.afewtoggles}"
                    OffContent="{x:Static prop:Resources.notspying}"
                    OnContent="{x:Static prop:Resources.spying}"/> `

### Progress Ring

` <mah:ProgressRing  IsActive="{Binding Path=IsLoading}" 
                          Grid.Column="1"
                          Grid.Row="2"
                          />`

### CheckBox

`  <CheckBox Content="{x:Static prop:Resources.one}"  Grid.Row="0" />`