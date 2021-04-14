# mahapps Metro einbinden

1. über NuGet-PaketManager installieren
2. in der view:
   1.   xmlns:mah="http://metro.mahapps.com/winfx/xaml/controls"
   2. <mah:MetroWindow...
3. in Code Behind *MainWindow:Window* zu *MainWindow:MetroWindow*

- um die Theme zu ändern, in App.xaml im ApplicationResources             <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Themes/Light.Steel.xaml" />     