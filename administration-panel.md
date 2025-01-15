## Admin Panel

### Default access:

In order to create contents in the admin panel we need to start the server and login as administrator.

```
URL: http://localhost:8080/reldens-admin
user: root@yourgame.com
password: root
```

By default, only the `root` registered user is an administrator.

### Change the default path `reldens-admin`:

In your project root folder look for the `.env` file and replace the value in the value for `RELDENS_ADMIN_ROUTE_PATH`:
```
RELDENS_ADMIN_ROUTE_PATH=/your-custom-admin-url
```

### Change the admin default role:

The admin role ID can be changed by setting the default "admin/roleId" in the "config" table in the database.

```sql
UPDATE `config` SET `value` = '[new-admin-role-id]' WHERE `scope` = 'server' AND `path` = 'admin/roleId';
```

That role has to be set in the user you want to be the administrator:

```sql
UPDATE `users` SET `role_id` = '[new-admin-role-id]' WHERE `email` = 'your-user@email.com';
```
