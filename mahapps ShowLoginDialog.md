# Show Login Dialog

- bei Start von PRogramm funkt. nicht (?)

- `  ShowLoginDialog(null, null);`

- ```c#
  private async void ShowLoginDialog(object sender, RoutedEventArgs e)
          {
              LoginDialogData result = await this.ShowLoginAsync("Authentication", "Enter your credentials", new LoginDialogSettings { ColorScheme = this.MetroDialogOptions.ColorScheme, InitialUsername = "MahApps" });
              if (result == null)
              {
                  //User pressed cancel
              }
              else
              {
                  if (result.Username == "admin" && result.Password == "admin")
                  {
   MessageDialogResult messageResult = await this.ShowMessageAsync("Authentication Information", String.Format("{0} succesfully logged in. ", result.Username));
                  }
                  else
                  {
                      MessageDialogResult messageResult = await this.ShowMessageAsync("LogIn-Error","Username or Password incorrect. Please try again.");
                      ShowLoginDialog(null, null);
                  }
                 
              }
          }
  
      }
  ```

  

