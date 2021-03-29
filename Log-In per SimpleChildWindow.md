# Log-In per SimpleChildWindow

```c#
<Grid>
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
                    
                    <Grid.RowDefinitions>
                        <RowDefinition Height="140"/>
                        <RowDefinition/>
                  
                    </Grid.RowDefinitions>
                    <Image Source="https://bracenet.net/wp-content/themes/bracenet/assets/images/bracenet-logo-hero-white.png"  
                           ToolTip="Bracenet" 
                           Grid.Row="0"
                           Grid.Column="0"
                        Margin="10"
                          />
                    <Grid Grid.Row="1" HorizontalAlignment="Center" VerticalAlignment="Top">
                        <Grid.RowDefinitions>
                            <RowDefinition Height="60"/>
                            <RowDefinition Height="60"/>
                            <RowDefinition/>
                        </Grid.RowDefinitions>
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition/>
                            <ColumnDefinition/>
                        </Grid.ColumnDefinitions>
                    <Label Content="{x:Static prop:Resources.username}"
                           Grid.Column="0"
                           Grid.Row="0"
                           Foreground="#f2f2f2"
                           HorizontalAlignment="Right"
                           Margin="5"
                           />
                    <Label Content="{x:Static prop:Resources.password}" 
                           Grid.Column="0"
                           Grid.Row="1"
                           Foreground="#f2f2f2"
                           HorizontalAlignment="Right"
                           Margin="5"
                           />
                    <TextBox 
                        Grid.Row="0"
                        Grid.Column="1"
                        Text="{Binding UserName}" 
                        Height=" 25" 
                        Width="200"
                        Margin="10" 
                        Background="#f2f2f2" 
                        mah:TextBoxHelper.Watermark="{x:Static prop:Resources.user}"
                       HorizontalAlignment="Left"
                       VerticalAlignment="Top"
                        />
               
                    <PasswordBox
                        mah:PasswordBoxBindingBehavior.Password="{Binding PassWord}"
                        mah:PasswordBoxHelper.CapsLockIcon="CAPS"
                        Grid.Row="1"
                        Grid.Column="1"
                        
                        Height=" 25" 
                        Width="200"
                        Margin="10" 
                        Background="#f2f2f2" 
                         HorizontalAlignment="Left"
                       VerticalAlignment="Top"
                                                />
                    <Label 
                        Grid.Row="0"
                        Grid.Column="1"
                        Content="{x:Static prop:Resources.userwrong}"
                        Margin="10,0,0,0"
                        FontSize="10"
                        Foreground="Red"
                        Visibility="{Binding UserExistNot, Converter={StaticResource BooleanToVisibilityConverter}}"
                        VerticalAlignment="Bottom"
                        
                        />

                    <Label 
                        Grid.Row="1"
                        Grid.Column="1"
                        Content="{x:Static prop:Resources.passwordwrong}"
                   
                        FontSize="10"
                        Foreground="Red"
                        Visibility="{Binding PassWrong, Converter={StaticResource BooleanToVisibilityConverter}}"
                        VerticalAlignment="Bottom"
                        Margin="10,0,0,0"
                        
                        />

                        <Grid Grid.Row="3" Grid.Column="1" HorizontalAlignment="Right">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition/>
                                <ColumnDefinition/>
                            </Grid.ColumnDefinitions>

                            <Button
                        Grid.Column="0"
                        Command="{Binding CancelLogInCMD}"
                        Content="{x:Static prop:Resources.cancel}"
                        FontSize="18"
                        Style="{DynamicResource MahApps.Styles.Button.Square}"
                        HorizontalAlignment="Right"
                        VerticalAlignment="Top"
                            Margin="10"
                        />

                            <Button
                        Grid.Column="1"
                        Grid.Row="3"
                        Command="{Binding LogInCMD}"
                        Content="{x:Static prop:Resources.login}"
                        FontSize="18"
                        Style="{DynamicResource MahApps.Styles.Button.Square}"
                        HorizontalAlignment="Left"
                        VerticalAlignment="Top"
                        Margin="10"                        
                        />

                        </Grid>
                    </Grid>
                   
                  
                </Grid>
            </simpleChildWindow:ChildWindow>


        </Grid>
```

