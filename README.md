# Reldens - Documentation

Version: 4.0.0

Project GitHub: https://github.com/damian-pastorini/reldens

Website: https://www.reldens.com/

Join us on Discord: https://discord.gg/HuJMxUY

Follow the project progress in the GitHub board: https://github.com/users/damian-pastorini/projects/2/views/1

### Sample game creation process:

- Install Reldens following the [installation guide](https://github.com/damian-pastorini/reldens-docs/blob/master/installation.md).
- Start the server and login into the admin panel (default URL http://localhost:8080/reldens-admin) to start creating the game contents.
```
user: root@yourgame.com
password: root
```
- Go to http://localhost:8080/reldens-admin/skills-levels-set.
Create as many "Levels Set"(s) you need. For this example, we need two since we will have two ["Class Paths"](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/class-path.md) (Warrior and Mage) with the "autofill" properties disabled.
- Go to http://localhost:8080/reldens-admin/skills-class-path. Create two "Class Path"(s):
    - key = warrior, label = Warrior, Level Set ID: 1
    - key = mage, label = Mage, Level Set ID: 2
- Use the game data generator (https://github.com/damian-pastorini/reldens-docs/blob/master/generators/players-experience-per-level.md) to create the players experience file or use the example one (https://github.com/damian-pastorini/reldens-docs/blob/master/examples/generate-data/players-experience-per-level.json).
- Import the generated file using the import command:
```
```
