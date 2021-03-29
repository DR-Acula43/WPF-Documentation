# Message requesten

- ein Objekt sendet eine Request ab und erhält darauf eine Antwort

- DiscoPageViewModel sendet beim Starten eine Request über einen neue Message/Channel und erhält darauf eine Antwort von MainWindowViewModel

## Message erstellen und requesten
1- Wie bei Senden zuerst eine Message erstellen, hier 

`public class ColorStateChannel : ValueChangedMessage<SolidColorBrush> { }`

2 - DiscoPageViewModel implementiert `:ObservableObject`

3- Im Konstruktor wird über den `WeakReferenceManager` die Request abgesendet und direkt in dem Binding BackgroundColor gespeichert

`BackgroundColor = WeakReferenceMessenger.Default.Send<Messages.ColorStateChannelRequest>();`

4- MainWindowViewModel bindet `:ObservableRecipient` (nicht Object, da es nicht sendet...reply zählt nicht)

5- in der OnActivated( )- Methode listened er auf den obigen Channel/ Message und sendet eine Antwort zurück. Dies ist der Wert der in das Binding gespeichert wird

`protected override void OnActivated()`
        `{`
           
            `WeakReferenceMessenger.Default.Register<Messages.ColorStateChannelRequest>(this, (r, m) =>
`            {
                ``m.Reply(BackgroundColor);`
`            });
            `

`base.OnActivated();`
        }