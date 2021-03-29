# ChangeCulture

​                

```c#
 public RelayCommand<string> ChangeCultureCmd => new(
             culture =>
             {
                 IsBusy = true;
             Configuration config = ConfigurationManager.OpenExeConfiguration(ConfigurationUserLevel.None);
             config.AppSettings.Settings["culture"].Value = culture;
             config.Save();
             Log.Verbose("Settings: changed culture to " + culture);
             Log.Information("Application restart required");
             IsBusy = false;
         },
         _ => !IsBusy
     );
```
- Beim ButtonPress muss das CommandParameter ="de" mitübergeben werden
- To-Do: Wie aktive Sprache ausgrauen