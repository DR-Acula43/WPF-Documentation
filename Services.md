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



### Services in ein Projekt einbinden

- Microsoft.Extensions.Hosting installieren
- Model AppSettings erstellen

App.xaml.cs

```c#
using Serilog;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Data;
using System.Diagnostics;
using System.Globalization;
using System.Linq;
using System.Threading.Tasks;
using System.Windows;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Configuration;
using ServicesAndSQLite.Services;
using Microsoft.Extensions.DependencyInjection;
using ServicesAndSQLite.Models;
using ServicesAndSQLite.ViewModels;
using ServicesAndSQLite.Views;

namespace ServicesAndSQLite
{
    /// <summary>
    /// Interaction logic for App.xaml
    /// </summary>
    public partial class App : Application
    {
        private readonly IHost host;

        public static IServiceProvider ServiceProvider { get; private set; }

        public App()
        {
            // loading UI/UX culture
            Configuration config = ConfigurationManager.OpenExeConfiguration(ConfigurationUserLevel.None);
            ServicesAndSQLite.Properties.Resources.Culture = new CultureInfo(config.AppSettings.Settings["culture"].Value);

            // global exception handler
            AppDomain.CurrentDomain.UnhandledException += AppDomainCurrentDomainUnhandledExceptionHandler;
            Dispatcher.UnhandledException += DispatcherUnhandledExceptionHandler;
            Application.Current.DispatcherUnhandledException += ApplicationCurrentDispatcherUnhandledExceptionHandler;
            TaskScheduler.UnobservedTaskException += TaskSchedulerUnobservedTaskExceptionHandler;

            // logging
            string outputTemplate = "[{Timestamp:HH:mm:ss} {Level:u3}] {Message:lj}{NewLine}{Exception}";
            Log.Logger = new LoggerConfiguration()
                    .ReadFrom.AppSettings()
                    .WriteTo.Debug(outputTemplate: outputTemplate)
                    .WriteTo.File("logs/app.log", outputTemplate: outputTemplate, rollingInterval: RollingInterval.Day, rollOnFileSizeLimit: true)
                    .CreateLogger();

            host = Host.CreateDefaultBuilder()  // Use default settings
                                                //new HostBuilder()          // Initialize an empty HostBuilder
                    .ConfigureAppConfiguration((context, builder) =>
                    {
                        // Add other configuration files...
                        builder.AddJsonFile("appsettings.local.json", optional: true);
                    }).ConfigureServices((context, services) =>
                    {
                        ConfigureServices(context.Configuration, services);
                    })
                    .ConfigureLogging(logging =>
                    {
                        // Add other loggers...
                    })
                    .Build();

            ServiceProvider = host.Services;
        }
        private void ConfigureServices(IConfiguration configuration, IServiceCollection services)
        {
            services.Configure<AppSettings>(configuration.GetSection(nameof(AppSettings)));
            //services.AddScoped<ISampleService, SampleService>();
            

            // Register all ViewModels.
            services.AddSingleton<MainViewModel>();

            // Register all the Windows of the applications.
            services.AddTransient<MainView>();
        }
        #region global exception handling
        private void TaskSchedulerUnobservedTaskExceptionHandler(object sender, UnobservedTaskExceptionEventArgs e)
        {
            GlobalExceptionHandler(e.Exception);
        }

        private void ApplicationCurrentDispatcherUnhandledExceptionHandler(object sender, System.Windows.Threading.DispatcherUnhandledExceptionEventArgs e)
        {
            GlobalExceptionHandler(e.Exception);
        }

        private void DispatcherUnhandledExceptionHandler(object sender, System.Windows.Threading.DispatcherUnhandledExceptionEventArgs e)
        {
            GlobalExceptionHandler(e.Exception);
        }

        private void AppDomainCurrentDomainUnhandledExceptionHandler(object sender, UnhandledExceptionEventArgs e)
        {
            GlobalExceptionHandler(e.ExceptionObject.ToString());
        }

        private void GlobalExceptionHandler(Exception ex)
        {
            Log.Error(ex, ex.Message);
        }
        private void GlobalExceptionHandler(string message)
        {
            Log.Error(message);
        }
        #endregion
        protected override async void OnStartup(StartupEventArgs e)
        {
            await host.StartAsync();

            var window = ServiceProvider.GetRequiredService<MainView>();
            window.Show();

            base.OnStartup(e);
        }

        protected override async void OnExit(ExitEventArgs e)
        {
            using (host)
            {
                await host.StopAsync(TimeSpan.FromSeconds(5));
            }

            base.OnExit(e);
        }
    }
}

```

IGetArtist.cs (Interface des Services)

```c#
namespace ServicesAndSQLite.Services
{
    public interface IGetArtist     //gbit vor was zu implementieren ist, das dann in anderen TEchnologien anders umgesetzt werden muss
    {
        string GetArtistID();
    }
}
```

GetArtist.cs (Implementation des Services)

```c#
namespace ServicesAndSQLite.Services
{
    public class GetArtist : IGetArtist
    {
        public int GetArtistID()
        {
            return -1;
        }
    }
}
```

MainViewModel.cs

```c#
public class MainViewModel : ObservableObject
    {
        public readonly IGetArtist getArtistImp;
    	
    public IFrameNavigationService FrameNavigationService { get; }

        public MainViewModel(IFrameNavigationService frameNavigationService, IGetArtist getArtist)
        {
            this.getArtistImp = getArtist;
            ...
        
```

- Aufrufen kann man den Service dann über `getArtistImp.GetArtistID()`

### Quelle

- [How do I connect a wpf application to sqlite database (microsoft.com)](https://social.msdn.microsoft.com/Forums/en-US/f8bfdd36-4019-4be3-aacd-42d863caa05a/how-do-i-connect-a-wpf-application-to-sqlite-database?forum=wpf)
- [Using the MVVM pattern in WPF applications running on .NET Core | Around and About .NET World (wordpress.com)](https://marcominerva.wordpress.com/2020/01/07/using-the-mvvm-pattern-in-wpf-applications-running-on-net-core/)
- 


