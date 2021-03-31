# PasswordBox mit Watermark

- Notdürftige Lösung, mit Label hinter transparenter PasswordBox, Content von LAbel wird "" sobald Passwort eingegeben wird
- View:

```xaml
<Label                      
                        Grid.Row="1"
                        Grid.Column="1"
                        Height=" 25" 
                        Width="200"
                        Margin="10" 
                        Background="#f2f2f2" 
                        HorizontalAlignment="Left"
                        VerticalAlignment="Top"         
                        Content="{Binding EnterPassw}"
                        FontSize="12"
                        Foreground="Gray"                           
                            />                       
                       
                        <PasswordBox
                        mah:PasswordBoxBindingBehavior.Password="{Binding PassWord}"
                        mah:PasswordBoxHelper.CapsLockIcon="CAPS"
                        Grid.Row="1"
                        Grid.Column="1"
                        Height=" 25" 
                        Width="200"
                        Margin="10" 
                        Background="Transparent" 
                        HorizontalAlignment="Left"
                        VerticalAlignment="Top"
                        VerticalContentAlignment="Center"                        
                        />
```

- ViewModel:

```c#
private string _enterPassw = Properties.Resources.enterpass;
        public string EnterPassw
        {
            get => _enterPassw;
            set => SetProperty(ref _enterPassw, value);
        }
...
private string _passWord="";
        public string PassWord
        {
            get => _passWord;
            set
            {
                SetProperty(ref _passWord, value);
                {
                    if (PassWord.Length != 0)
                    {
                        EnterPassw = "";
                    }
                    else if (PassWord.Length == 0)
                    {
                        EnterPassw = Properties.Resources.enterpass;
                    }
                    OnPropertyChanged(nameof(EnterPassw));
                }
            }
        }
```

