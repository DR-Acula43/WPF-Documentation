# Expander

- Ein paar Beispiele zu dem expander Element 

  

```c#
<Expander Margin="10" Grid.Row="1"  Background="LightBlue" >
            <Expander.Header>
                <BulletDecorator>
                    <BulletDecorator.Bullet>
                        <Image Width="50" Source="https://weneedfun.com/wp-content/uploads/2016/07/Most-Beautiful-Sunset-Pictures-13-1024x767.jpg"/>
                    </BulletDecorator.Bullet>
                    <TextBlock Foreground="White" FontFamily="Arial" >Header mit bild</TextBlock>
                </BulletDecorator>
            </Expander.Header>
            <ScrollViewer Height="100">
            <TextBlock Foreground="orange" TextWrapping="Wrap" FontSize="18" >
                The Content of the Expander can only be one control, like in our first example where we use a TextBlock control, but nothing prevents you from making this e.g. a Panel, which can then hold as many child controls as you want it to. This allows you to host rich content inside your Expander, from text and images to e.g. a ListView or any other WPF control.

                    Here's an example of more advanced content, where we use several panels, text and an image and even a TextBox control:
            </TextBlock>
            </ScrollViewer>

        </Expander>
```

- Expander mit Buttons

```c#
<Expander Margin="10" ExpandDirection="Right" Grid.Row="2" Header="Mit Buttons">
        
                <Grid>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition/>
                        <ColumnDefinition/>
                    </Grid.ColumnDefinitions>
                    <Grid.RowDefinitions>
                        <RowDefinition/>
                        <RowDefinition/>
                       
                    </Grid.RowDefinitions>

                
                <Button Grid.Row="0" Grid.Column="0" Content="Button 1"/>
                <Button Grid.Row="1" Grid.Column="0" Content="Button 2"/>
                <Button Grid.Row="0" Grid.Column="1" Content="Button 3"/>
                <Button Grid.Row="1" Grid.Column="1" Content="Button 4"/>
            </Grid>

        </Expander>
```

