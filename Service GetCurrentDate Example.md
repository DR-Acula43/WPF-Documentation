# Service GetCurrentDate Example

- Benutzt ViewModelBase, NICHT ObservableObject!
- in App.xaml.cs ServiceProvider definieren; jeden SErvice hinzufügen `            services.AddScoped<ISampleService, SampleService>();`
- Im ViewModel Attribut vom Typ des Interfaces erstellen `private readonly ISampleService sampleServiceTest;`
- über das `sampleServiceTest`kann man nun auf die Methode GetCurrentDate() zugreifen