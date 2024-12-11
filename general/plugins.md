## Plugins

In Reldens you will find two types of plugins, "core-plugins" and your "custom-plugins".

### Core plugins

Core plugins are inside the project source (in the "lib" folder), and contain a specific structure which is used to determine:
- if the plugin is enabled or not
- if it has implementations for the server side, the client or both
 
This way in a single plugin you can have a complete feature.

To enable/disabled a plugin you need to include it in the features lists, both in the files from the "feature" plugin, and in the database in the "features" table. 

A normal core-plugin folder will look like this:

/[plugin-name]/ > where you can also drop shared files for both server and client (like constants)
/[plugin-name]/server > folder where you will have all your server logic
/[plugin-name]/server/plugin.js > server configuration file to initialize the plugin server logic
/[plugin-name]/client
/[plugin-name]/client/plugin.js > client configuration file to initialize the plugin server logic

For example: the inventory plugin https://github.com/damian-pastorini/reldens/tree/master/lib/inventory.

Most of these plugins could be enabled/disabled or override, but note this will have a high impact on the amount of customizations you will need to make in order to allow the platform to fully work.


### Custom plugins

These can be found in [your-project-folder]/theme/plugins.

There you will see the "client-plugin.js" and "server-plugin.js" files from where you can customize your project by listening events, adding custom classes, etc.
