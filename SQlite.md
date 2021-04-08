# SQLite

- man braucht natürlich zuerst eine Tabelle (chanook.db downloaden oder z.B. mit sqlite studio eine erstellen)
- zu installieren in NuGet:
  - System.Data.SQLite

## Verbindung zu Datenbank herstellen

- hier wird eine Verbindung zu einer lokalen DB hergestellt und aus der Tabelle *Users* die Columns *uName* und *uID* gelesen

```c#
using (SQLiteConnection conn = new SQLiteConnection(@"Data Source=C:\Users\Simon Weber Work\Documents\GitHub\Services-Plus-SQLite\WpfNetCoreMvvm\Management.db;"))
            {
                conn.Open();

                SQLiteCommand command = new SQLiteCommand("Select * from Users", conn);
                SQLiteDataReader reader = command.ExecuteReader();

                string curUName;
                int curUID;

                while (reader.Read())
                {
                    curUName = reader["uName"].ToString();
                    curUID = int.Parse(reader["uID"].ToString());
                    UserList.Add(new User() { UID = curUID, UName = curUName });
                }


                reader.Close();
            }
```

### Create

```c#
public void createUser(int id, string name)
        {
            using (SQLiteConnection conn = new SQLiteConnection(@"Data Source=C:\Users\Simon Weber Work\Documents\GitHub\Services-Plus-SQLite\WpfNetCoreMvvm\Management.db;"))
            {
                conn.Open();

                SQLiteCommand command = new SQLiteCommand($"INSERT INTO Users(uID, uName) VALUES ({id},'{name}')", conn);
                command.ExecuteNonQuery();
            }
        }
```

### Update

```c#
 public void updateUser(int id, string newName)
        {
            using (SQLiteConnection conn = new SQLiteConnection(@"Data Source=C:\Users\Simon Weber Work\Documents\GitHub\Services-Plus-SQLite\WpfNetCoreMvvm\Management.db;"))
            {
                conn.Open();
                SQLiteCommand command = new SQLiteCommand($"UPDATE Users SET uName = '{newName}' WHERE uID = {id}", conn);
                command.ExecuteNonQuery();
            }
        }
```

### Delete

```c#
public void deleteUser(int id)
        {
            using (SQLiteConnection conn = new SQLiteConnection(@"Data Source=C:\Users\Simon Weber Work\Documents\GitHub\Services-Plus-SQLite\WpfNetCoreMvvm\Management.db;"))
            {
                conn.Open();
                SQLiteCommand command = new SQLiteCommand($"DELETE FROM Users WHERE uID ='{id}'", conn);
                command.ExecuteNonQuery();
            }
        }
```

