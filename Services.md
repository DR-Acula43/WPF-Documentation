# Services

- Services bieten jeweils eine spezielle Funktionalität für Views in MVVM Anwendungen

- definiert in Views(XAML) - kann trotzdem von ViewModels benutzt werden

- Service ist ein  Behavior, dass ein Interface implementiert

- -> Services machen es einfach Unit-Tests zu implementieren

- Man schreibt eine App für PC die ShowDialog macht, dann will man sie auf Android exportieren; hat aber andere API für ShowDialog

  -> mit Services will man erreichen, das im ViewModel beschrieben wird was gemacht wird, ohne es tatsächlich zu tun

- Man erstellt ein Interface, die Implementierung dieses Interfaces sieht dann aber auf jeder Plattform anders aus



```c#
public interface IDialogService
{
    Task ShowDialogAsync(string message);
}
```



```c#
public class DialogService: IDialogService
{
    public async Task ShowDialogAsync(string message)
    {
        MessageDialog dialog = new MessageDialog(message);
        await dialog.ShowAsync();
    }
}



```

Im ViewModel:

```c#

        private readonly ISampleService sampleServiceTest;
        private readonly AppSettings settings;
...
 public MainViewModel(ISampleService sampleService,
            IOptions<AppSettings> options, IWriteSomething writeSomething)
        {
            this.sampleServiceTest = sampleService;
            settings = options.Value;

            this.writeSomething = writeSomething;
            
            ExecuteCommand = new RelayCommand(async () => await ExecuteAsync());
        }

        private Task ExecuteAsync()
        {
            Debug.WriteLine(sampleServiceTest.GetCurrentDate());
            Debug.WriteLine(writeSomething.WriteSomethingAsString("as string"));
            CurTime = sampleServiceTest.GetCurrentDate();
            OnPropertyChanged(nameof(CurTime));
            return Task.CompletedTask;
        }
```



In App.xaml.cs



```c#
private void ConfigureServices(IConfiguration configuration, IServiceCollection services)
        {
            services.Configure<AppSettings>(configuration.GetSection(nameof(AppSettings)));
            services.AddScoped<ISampleService, SampleService>();
            services.AddScoped<IWriteSomething, WriteSomething>();

            // Register all ViewModels.
            services.AddSingleton<MainViewModel>();

            // Register all the Windows of the applications.
            services.AddTransient<MainWindow>();
        }
```







### Quelle

- [How do I connect a wpf application to sqlite database (microsoft.com)](https://social.msdn.microsoft.com/Forums/en-US/f8bfdd36-4019-4be3-aacd-42d863caa05a/how-do-i-connect-a-wpf-application-to-sqlite-database?forum=wpf)
- [Using the MVVM pattern in WPF applications running on .NET Core | Around and About .NET World (wordpress.com)](https://marcominerva.wordpress.com/2020/01/07/using-the-mvvm-pattern-in-wpf-applications-running-on-net-core/)
- 









-----------------------------------------------------------------------------------------------------------------------------------------------------------



#### Service in View einbinden 

Code 1

```xaml
<UserControl x:Class="Example.View.DocumentView"
    xmlns:dx="http://schemas.devexpress.com/winfx/2008/xaml/core"
    xmlns:dxmvvm="http://schemas.devexpress.com/winfx/2008/xaml/mvvm"
    xmlns:ViewModel="clr-namespace:Example.ViewModel" ...>
    <UserControl.DataContext>
        <ViewModel:DocumentViewModel/>
    </UserControl.DataContext>
    <dxmvvm:Interaction.Behaviors>
        <dx:DXMessageBoxService/>
    </dxmvvm:Interaction.Behaviors>
    ...
        <Button Content="Close Document" Command="{Binding CloseDocumentCommand}" .../>
    ...
</UserControl>
```

- die DXMessageBoxService Klasse wird zu den *Interaction.Behaviors* hinzugefügt
- Services sind dann automatisch in den ViewModels *injected* , man kann also in den VM die `GetService<T> `benutzen, die dann ein *Interface* returnt um auf den *DXMessageBoxService* 
- `GetService<T> ` ist von `ViewModelBase`, wir implementieren stattdessen `ObservableObject`

Code 2

```c#
public class DocumentViewModel : ViewModelBase {
    public ICommand CloseDocumentCommand { get; private set; }
    public IMessageBoxService MessageBoxService { get { return GetService<IMessageBoxService>(); } } //auf Interface zugreifen
    ...
    void CloseDocument() {		//Interface Methode verwenden
        MessageBoxResult canCloseDocument = MessageBoxService.Show(
            messageBoxText: "Want to save your changes?", 
            caption: "Document", 
            button: MessageBoxButton.YesNoCancel);
        if(canCloseDocument == MessageBoxResult.Yes) {
            //...
        }
    }
}
```



### Schritte um Services zu verwenden

1. *DataContext* der *View* zum *ViewModel* (wie immer)
2. den Service in *XAML* definieren (Code 1)
3. Aus dem *ViewModel* via `GetService<T>` Zugriff auf *Interface* des *Services* bekommen (Code 2)



## Services in custom ViewModels

- Um Services nutzen zu können, muss man das *ISupportServices* Interface in das *ViewModel* implementieren
- Dieses Interface enthält einfach eine Get-Methode
- Das Interface wird wie folgt implementiert

Code 3

```c#
public class ViewModel : ISupportServices {
    IServiceContainer serviceContainer = null;
    protected IServiceContainer ServiceContainer {
        get {
            if(serviceContainer == null)
                serviceContainer = new ServiceContainer(this);
            return serviceContainer; 
        }
    }
    IServiceContainer ISupportServices.ServiceContainer { get { return ServiceContainer; } }
}
```

- Die *ServiceContainer* Klasse implementiert das Interface *IServiceContainer* mit dem man auf *Services* zugreifen kann

- Das *IServiceContainer* Interface hat GetService und RegisterService Methoden

- wenn Services in einer View definiert werden, analysieren sie deren DataContext

  -> finden sie ein ISupportServices-Objekt dort, registriert sich der Service an diesem Objekt mit RegisterService

  ​	-> Service wird verfügbar an dem ISupportServices-Objekt via IServiceContainer.GetService<T>





## Quellen

- [Getting Started | WPF Controls | DevExpress Documentation](https://docs.devexpress.com/WPF/17444/mvvm-framework/services/getting-started)
- 