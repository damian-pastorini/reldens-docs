## Known issues


### Connection errors with MySQL:

If NodeJS can't connect to your MySQL server is highly likely you are using a new version of MySQL authentication (schema vs native).
In that case make sure to have `mysql2` been set as your RELDENS_DB_CLIENT environment variable in the `.env` and in the `knexfile.js` files.

If you still see the issue, you can try by updating your DB user to use the old MySQL "native" password:
```sql
ALTER USER '<YOUR_USERNAME>'@'<YOUR_HOST>' IDENTIFIED WITH mysql_native_password BY '<YOUR_PASSWORD>';
```

Or create a new one with it:
```sql
CREATE USER '<YOUR_USERNAME>'@'<YOUR_HOST>' IDENTIFIED WITH 'mysql_native_password' BY '<YOUR_PASSWORD>';
```
