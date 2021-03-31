# Shadow

```c#
 <Grid >
            <Border Background="#70000000"
        Margin="0"
        Visibility="{Binding IsBusy, Converter={StaticResource BooleanToVisibilityConverter}}">
                <Border.Effect>
                    <DropShadowEffect Opacity="2"/>
                </Border.Effect>
            </Border>
        </Grid>
```

```
<Label Content ="Shadow"/>
            <Label.Effect>
                <DropShadowEffect
                         ShadowDepth="5"
                         Direction="330"
                          Color="Black"
                            Opacity="0.3"
                         BlurRadius="4"/>
            </Label.Effect>
        </Label>
```

