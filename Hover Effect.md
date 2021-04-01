# Hover-Effect am Beispiel einer Tile

```c#
<mah:Tile ToolTip="{x:Static prop:Resources.adressbook}" Grid.Column="0" Grid.Row="0" Background="Orange" Command="{Binding GoToAdressCMD}"  Width="Auto" Height="Auto"  Title="{x:Static prop:Resources.adressbook}" Foreground="White" HorizontalTitleAlignment="Right"
                 FontSize="40"  FontFamily="Arial" >
                    <Viewbox Margin="100,70,70,70"  MaxWidth="175" >
                    <Canvas Width="24" Height="24"  >
                            <iconPacks:PackIconMaterial Kind="BookOpenOutline"  >
                                <iconPacks:PackIconMaterial.Effect>
                                    <DropShadowEffect
                         ShadowDepth="3"
                         Direction="330"
                          Color="Black"
                            Opacity="0.3"
                         BlurRadius="4"/>

                                </iconPacks:PackIconMaterial.Effect>
                            </iconPacks:PackIconMaterial>
                        </Canvas>
                </Viewbox>
                    <mah:Tile.Style>
                        <Style TargetType="mah:Tile" >
                            <Setter Property="Background" Value="#f2f2f2"/>
                            <Style.Triggers>
                                <Trigger Property="IsMouseOver" Value="True">
                                    <Setter Property="Margin" Value="-2.5"/>

                                    <Setter Property="BorderBrush" Value="Transparent"/>
                                </Trigger>
                            </Style.Triggers>
                        </Style>
                    </mah:Tile.Style>
                </mah:Tile>
```

