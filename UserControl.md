# UserControl

- mehrere Objekte die zusammengehörig sind kann man in eine UserGroup schreiben
- ist wiedervertwertbar, wenn es öfter im Projekt vorkommt zB
- [Creating & using a UserControl - The complete WPF tutorial (wpf-tutorial.com)](https://www.wpf-tutorial.com/usercontrols-and-customcontrols/creating-using-a-usercontrol/)



## Implementierung

- Ordner UserControls Add -> new UserControl
  - hier die UC einmal als als Vorlage schreiben
- Im CodeBehind *this.DataContext=this;* in Konstruktor schreiben und gewünschte Attribute/ Bindings definieren