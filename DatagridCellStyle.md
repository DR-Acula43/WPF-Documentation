# DatagridCellStyle




```c#
 				<DataGrid.CellStyle>
                    <Style TargetType="DataGridCell">
                        <Style.Triggers>
                            <Trigger Property="IsSelected" Value="True">
                                <Setter Property="Foreground" Value="Orange"/>
                                <Setter Property="Background" Value="#f2f2f2"/>
                            </Trigger>
                        </Style.Triggers>
                    </Style>
                </DataGrid.CellStyle>
```

- funktioniert analof auch mit DataGrid.RowStyle