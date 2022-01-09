# Slime Skies – SkyBlock meets Create

.. is a SkyBlock style modpack for [Minecraft] 1.16.5 (Java Edition) which uses [Create] for a very uniquely different beginning in a void world. Start out with just a tree, a campfire, andesite, zinc and kelp. Explore 16 biome-themed islands to gain access to more plants and animals, as well as the Nether and End.

![](docs/screenshot.png)

Be wary, this pack is still a **work in progress!** While it should be possible to build amazing mechanical- and redstone-powered automatons, there are some elements not yet finished: Not all islands have been built, you can't yet get to the End, and some items like diamonds and netherite are unobtainable.


## Download / Installation

The modpack is currently only available as a **self-updating** MultiMC instance.

- Download and install [MultiMC] if you don't have it already.
- Drag the following link into the main window of MultiMC, and press "OK".  
  [`https://meowface.org/copygirl/Slime Skies.zip`](https://meowface.org/copygirl/Slime%20Skies.zip)  
  Alternatively, create a new instance, select "Import from zip" and enter the above URL.
- Start the game! At first launch, [packwiz] downloads all the config files and mods for you. When the modpack updates, the MultiMC instance will also update by itself with newly added / removed / updated mods, changed recipes, etc.

There is one copy of the world available in the singleplayer world selection screen. Because I could not find a mod that creates new worlds from a template, if you want to start over from scratch, you will have to follow these steps:

- In MultiMC, select the instance and click "Minecraft Folder" on the right.
- Copy the `world_template` folder into your `saves` folder, and rename it.
- The `world_template` folder will automatically update with the modpack.

Unfortunately, there currently is no way to update a world you've already played with new or improved world content, such as new islands. (Unless you want to go through the effort of using a 3rd party map editor such as [Amulet] to copy them in.) You've been warned about the work-in-progress nature of this pack!

### Updating

For some updates, we update the required Forge version. Unfortunately, packwiz is unable to update this automatically for us. So when you update the modpack, you might have to update the Forge version used by MultiMC manually. No worries though, it is very simple!

- Right click the instance in MultiMC and select "Edit Instance"
- Select the "Version" tab on the left.
- Click the "Install Forge" button on the right.
- Select the version found in [`pack.toml`](pack.toml), currently `36.2.23`.

And you're done! Enjoy the update!


## Server Setup

We're using [packwiz] to for developing the modpack and providing the files, such as mods, configs, the world map, ... So go ahead and grab the latest bootstrap `.jar` from its [GitHub Releases page][packwiz-releases], as well as [Forge for 1.16.5][forge-download] - the recommended version can be found in the [`pack.toml`](pack.toml).

```sh
# Adjust if necessary, such as if a new version is available / required.
wget https://github.com/comp500/packwiz-installer-bootstrap/releases/download/v0.0.3/packwiz-installer-bootstrap.jar
wget https://maven.minecraftforge.net/net/minecraftforge/forge/1.16.5-36.2.23/forge-1.16.5-36.2.23-installer.jar

# Download modpack files. Also run this to update.
java -jar packwiz-installer-bootstrap.jar -g -s server https://raw.githubusercontent.com/copygirl/slime-skies/main/pack.toml

# Download Minecraft and Forge files.
java -jar forge-1.16.5-36.2.23-installer.jar --installServer

# IMPORTANT! Before starting up the server, make sure
# copy the folder `world_template` and name it `world`.

# Now do the usual, accept the EULA, edit your server
# properties, run your startup script as you're used to.
java -jar -Xmx4G -Xms4G forge-1.16.5-36.2.23.jar nogui
```


## Development

To build a MultiMC instance .zip file, run [`./build_multimc.sh`](build_multimc.sh). Due to most files being served through packwiz, the .zip only needs to be updated when files in `include` or `world_template` are changed.

Working on the modpack requires the [packwiz] tool, so be sure to download it first.
```sh
packwiz update --all # Update all mods to latest.
packwiz refresh      # Run after modifying any files.
git commit -a        # Now you can commit your changes..
git push             # ..and push them to the repository.
```

If you want to do local testing:

- Set the MultiMC instance's "pre-launch command" to:  
  `http://localhost:8080/pack.toml`
- Run `packwiz serve` to run a simple webserver that serves the files.  
  This will also update index automatically on file changes.
- Launch the instance and it will pull changes from your local setup.  
  Note that many changes can be applied by running `/reload` in-game.


[Minecraft]: https://minecraft.net/
[Create]: https://curseforge.com/minecraft/mc-mods/create
[MultiMC]: https://multimc.org/
[Amulet]: https://www.amuletmc.com/
[packwiz]: https://github.com/comp500/packwiz
[packwiz-releases]: https://github.com/comp500/packwiz-installer-bootstrap/releases
[forge-download]: https://files.minecraftforge.net/net/minecraftforge/forge/index_1.16.5.html
