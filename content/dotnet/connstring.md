# Connection strings

| Description | Value |
| :---: | :---: |
| Connection with windows auth | `new SQLConnection("Server=localhost; atabase=master;Trusted_Connection=true;");` |
| Connection with sql server auth | `new SQLConnection("Server=localhost;database=master;User ID=user;Password=password;");` |
| Azure type connections  | `new SQLConnection("Server=tcp:mydatabase.database.windows.net,1433;Initial Catalog=myDb;Persist Security Info=False;User ID=userid;Password=password;Encrypt=True;");` |
| Add Mars, connectionTimeout  | `new SQLConnection("Server=tcp:mydatabase.database.windows.net,1433;Initial Catalog=myDb;Persist Security Info=False;User ID=userid;Password=password;Encrypt=True;Connection Timeout=30;MultipleActiveResultSets=True;");` |
