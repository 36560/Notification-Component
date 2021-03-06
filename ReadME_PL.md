# Komponent powiadomień (MVC) .NET przy użyciu Hangfire i Postal

## Wersje
 - .Net Framework v4.8
 - Hangfire 1.7.22
 - Poczta.Mvc4.1.2.0

## Opis:

 Komponent umożliwia wysyłanie zaplanowanych wiadomości e-mail do użytkowników w aplikacjach Task/ToDo (web).
Może służyć jako przypomnienie o zapomnianych/dzisiejszych/przyszłych zadaniach lub zdarzeniach dla każdego użytkownika. Deweloper może również zezwolić użytkownikom na skonfigurowanie tej opcji,
a następnie użytkownik może np. wybrać opcję, aby otrzymywać powiadomienia tylko o przyszłych zadaniach.

## Konfiguracja
### Web.config
 Musisz zainstalować Hangfire i Postal v4 (dla platformy .Net 4) porzez NuGet. W web.conf ustaw swój adres e-mail serwera (z tego adresu e-maile będą wysyłane do każdego użytkownika). 
 To przykład dla Gmaila:
 
 ![nowy1](https://user-images.githubusercontent.com/67658221/127113257-62e10bc1-d4cb-4fad-803e-66ff3499e944.PNG)

````
<system.net>
    <Ustawienia poczty>
      <smtp from="twoja poczta@gmail.com">
        <network host="smtp.gmail.com" port="587" userName="twoja poczta@gmail.com" password="twoje hasło" enableSsl="true" />
      </smtp>
    </mailSettings>
</system.net>
````

### Startup.class
  Utwórz klasę startową OWIN, jeśli jej nie masz. Następnie wywołaj te metody:
  
 ```
 public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             //your other methods like connection with database
             app.UseHangfireDashboard();
             app.UseHangfireServer();            
         }
     }
```
 
#### Notatka:
 Jeśli korzystasz z konta Google, musisz włączyć specjalną opcję: https://support.google.com/accounts/answer/6010255?hl=pl. Umożliwia ona korzystanie z poczty e-mail we własnych aplikacjach.
 
 ### Połączenie z bazą danych, aktualny użytkownik i opcje powiadomień
  Na swój sposób musisz uzyskać połączenie z bazą danych oraz adres e-mail aktualnie zalogowanego użytkownika. W bazie możesz zapisać również opcję powiadomień dla każdego użytkownika lub ustawić domyślną dla całej aplikacji.
 Więcej o opcjach powiadomień znajdziesz poniżej w rozdziale o korzystaniu z komponentu.
 
 
 ## Dołączanie komponentu do projektu

 Komponent zawiera:
 - Noti.cs (dodaj to do folderu modelu) MODEL
 - Noti.cshtml (po zainstalowaniu Postal dodaj to do folderu Views/Emails) VIEW
 - NotiController.cs (dodaj to do folderu kontrolera) KONTROLER


 W Noti.cshtml zmień pierwszą linię dla przestrzeni nazw modelu Noti:
 
 ```
  @model YourProjectName.NameofFolderwithModel.Users.Noti
  To: @Model.UserEmail
  Subject: @Model.Info

  <p>This task waiting for you. Go to the app to complete it.</p>
  @foreach (string item in @Model.TaskList)
  {
      <p> >> @item</p><br>
  }
 ```
 
 ## Korzystanie z komponentu
  Utwórz instancję NotificationController w miejscu, w którym chcesz uruchomić komponent powiadomień (np. w kontrolerze dla strony po poprawnym zalogowaniu).
  
  ````
  NotiController notiController2 = nowy NotiController();
  ````


## Download
- przykładowy projekt (z użyciem wbudowanej bazy sql)
- tylko komponent powiadomień

## Przydatne linki
Dokumentacja Hangfire: https://docs.hangfire.io/en/latest/
Dokumentacja w języku ANG:

