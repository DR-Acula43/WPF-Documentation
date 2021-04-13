# Services

- Services sind Komponenten die man in Programmen verwendet
- Es gibt Interfaces, die vorgeben wie die Schnittstellen aussehen müssen, konkrete Implementierung kann dann von Technik zu Technik unterschiedlich aussehen

## Services implementieren

- Im Folgenden wird gezeigt, wie man einen Service implementiert (hier in ein Projekt mit der Project Template *WPF MVVM App (.Net 5.0)*)
- für den genauen, dokumentierten Code bitte in XXX schauen

### Service Interface erstellen

- man erstellt ein Interface, das alle Methode hat die der Service später implementieren soll
- *ISampleService.cs*

### Service implementieren

- diese Implementation sieht von Einsatzgebiet zu Einsatzgebiet anders aus und ist im Idealfall, die einzige Komponente, die ausgetauscht werden muss
- *SampleService.cs*

### MainViewModel

- wichtige Stellen im Code sind mit *//!!!* markiert
- Service wird als Attribut der Klasse definiert und kann hier verwendet werden
- *MainViewModel.cs*

### ViewModelLocator

- wichtige Stellen im Code sind mit *//!!!* markiert
- hier werden dem ViewModel die Services zugewiesen
- *ViewModelLocator.cs*

### App.xaml

- nötige namespaces einbinden und ViewModelLocator definieren
- *App.xaml*

### App.xaml.cs

- hier muss man alle Services registrieren

- Achtung! Bei dem verwendeten Template auch zusätzlich den *IFrameNavigationService* 

- über NuGet-Paketmanager *Microsoft.Extensions.Hosting* importieren

- wichtige Stellen im Code sind mit *//!!!* markiert

- *App.xaml.cs*

  

