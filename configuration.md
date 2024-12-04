### System Configuration

This is the "general settings" area where you can manage a lot of the platform options.

In these records you can specify:
 
The "scope":
  - "server": all the internal game setup, not shared to the clients.
  - "client": all the public config information broadcast to everyone.

A "path":
- A string value that will be converted to an objects-properties tree.
For example "actions/skills/affectedProperty" will be accessible on `config.actions.skills.affectedProperty`.

A "value":
This will be always a string that will be converted by the config "type".

The "type":
One of the available (but editable from the admin), string, float, boolean, json or comma separated. 
