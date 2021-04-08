# Services

- Services sind Komponenten die man in Programmen verwendet
- Es gibt Interfaces, die vorgeben wie die Schnittstellen aussehen müssen, konkrete Implementierung kann dann von Technik zu Technik unterschiedlich aussehen

### Interface von Service

```c#
using System;
using System.Collections.Generic;
using System.Text;
using WpfNetCoreMvvm.Models;

namespace WpfNetCoreMvvm.Services
{
   public interface IUsers
    {
        public List<User> getAllUsers();
        public string getNameByID(int id);
        public int getIDByName(string name);
        public List<int> getAllGroupIDByUser(int id);
        public void createUser(int id, string name);
        public void deleteUser(int id);
        public void updateUser(int id,string newName);

    }
}
```

### Implementierung des Interfaces (der eigentliche Service)

```c#
namespace WpfNetCoreMvvm.Services
{
    public class Users : IUsers
    {

        public List<User> getAllUsers()
        {...
        }

        public int getIDByName(string name)
        {...
        }

        public string getNameByID(int id)
        {...
        }

        public List<int> getAllGroupIDByUser(int id)
        {...
        }

        public void createUser(int id, string name)
        {...
        }

        public void deleteUser(int id)
        {...
        }
        
        public void updateUser(int id, string newName)
        {...
    }
}
```

### In App.xaml.cs Service hinzufügen

```c#
 public static IServiceProvider ServiceProvider { get; private set; }

        public App()
        {
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
            services.AddScoped<ISampleService, SampleService>();
            services.AddScoped<IGroupsService, GroupsService>();

            services.AddScoped<IUsers, Services.Users>();

            // Register all ViewModels.
            services.AddSingleton<MainViewModel>();

            // Register all the Windows of the applications.
            services.AddTransient<MainWindow>();
        }

        protected override async void OnStartup(StartupEventArgs e)
        {
            await host.StartAsync();

            var window = ServiceProvider.GetRequiredService<MainWindow>();
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
```



### Im ViewModel Service Benutzen

```c#
public class MainViewModel : Microsoft.Toolkit.Mvvm.ComponentModel.ObservableObject, INotifyPropertyChanged
    {
        private readonly IUsers users;
    
         public MainViewModel(IOptions<AppSettings> options, IUsers users)
        {      
           this.users = users;
             
            users.createUser(11, "Dwight");     
         }
    ...
}
```

