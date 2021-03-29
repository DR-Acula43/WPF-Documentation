# SimpleChildWindow

```c#
 <simpleChildWindow:ChildWindow x:Name="child01"
                                       CloseByEscape="false"
                                       IsEnabled="True"
                                       IsOpen="{Binding LoggedIn,  Converter={StaticResource BoolInverter}}"
                                      Background="Transparent"
                                       HorizontalContentAlignment="Stretch"
                                       VerticalContentAlignment="Stretch"
                                       Padding="15"       
                                           ShowTitleBar="False"
                                      >
                <Grid Background="Orange" Width="600">
                    <!-- child content here -->
                </Grid>
</simpleChildWindow:ChildWindow>
```

