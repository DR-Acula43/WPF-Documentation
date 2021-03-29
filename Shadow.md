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

