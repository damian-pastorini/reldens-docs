## Project structure

To analyze the folder structure we are going to check the skeleton project, which is how your project will look:

https://github.com/damian-pastorini/reldens-skeleton

After you installed Reldens you are going to see is the following:

#### - [project-root]/theme/default

This is the default theme of the Platform. It's used on the demo, and we keep it there for the base installation of the project.

If you look at the platform repository (/theme/default) this is the only theme folder you will see.

In the skeleton repository we included some build scripts in the package file to help developer with the project initialization.

https://github.com/damian-pastorini/reldens-skeleton/blob/master/package.json


#### - [project-root]/theme/packages

This is where all your custom project classes should go.

This also can be found as the only packages folder in the platform repository (/theme/packages).

In this folder you will find the client and server JS files where you can define all your custom classes.

By default, you will see all the demo examples of each class group (objects, inventory, skills, for now).


#### - [project-root]/theme/custom-game-theme-test

As you can see this folder doesn't exist in the platform repository (/theme), and that's because it's created just as an example on how you could create your own themes.


#### - [project-root]/dist

This is where the default bundler (Parcel) will generate the project public files.

This is the generated "client-side" of your project, which can be uploaded anywhere (like any CDN), so you can distribute your game and from there connect to your server.
