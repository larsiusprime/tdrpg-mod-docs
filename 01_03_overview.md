##1.3 File system overview

Mods are simply a collection of data and graphic files organized in a certain structure.
When you’re running a mod, any time the game needs a certain asset it will first look in your mod for the file.
If it doesn’t find it, it will revert to the default version of that file.

Example:You can create a valid mod that consists of nothing but a single sprite sheet graphic of Azra with a
blue dress instead of a purple one. When the game looks for Azra’s spritesheet, it will load your changed version, 
and Azra will have a blue dress in battle. Whenever the game looks for anything else, it won’t find the file in your
mod, so it will use the default version of that file instead, so your mod will be exactly the same as the normal game,
except Azra will have a blue dress.

When you export a mod for the first time, you can specify how much data you want to include. Since large graphic files
can take a long while to export (particularly cutscene and background assets), if you don’t feel like changing those in
your mod, it’s best to stick with just data, or just data and sprites. If you later decide you do want to make changes to
those heavier graphicd files, you can always add them later, but you’ll need to get the filenames and folder structure right.
In this case it’s best to do a separate full graphics-and-everything export to a new mod folder with a different name, and 
then copy over the missing assets. This way, you can avoid overwriting your existing work.

Below is the structure of a fully-exported mod that contains all the game’s data.

The root directory contains these folders:

```
  audio/       ← sound effects & music
  fonts/       ← true type fonts
  gfx/         ← graphics (more on this later)
  locales/     ← localization data (all the game's user-facing text)
  maps/        ← level data & image maps, as well as original style overworld data
  monologue/   ← branching dialogue trees (only used for the "bonus goodies" & "secrets" pop ups currently)
  tables/      ← .tsv tables for character class stats, etc
  tiled/       ← HD overworld data
  xml/         ← assorted data files
```

The `\maps` and `\tables` folders contain some very important files:

```
  maps\index.xml              ← game index (very important!)
  maps\<level_id>.png         ← image map for level
  maps\<level_id>.xml         ← data file for level
  maps\<overworld_<xyz>.png   ← overworld tile layout (original art mode)
```

```
   tables\exp.csv             ← global character levelup table
   tables\recruit.csv         ← new recruit cost table
   tables\<class_name>.xml    ← character class stats table
```

The `/xml` folder contains most of the game's "core" data files. 

It has these subfolders:
```
  entities/           ← graphics metadata
  options/            ← options data
  scenes/             ← cutscene & puppet show scripts
  ui/                 ← user interface layouts
```
  
And these significant files:
```
  achievements.xml      ← achievement definitions
  actions.json          ← game input action definitions
  bonus.xml             ← bonus challenge levels
  credits.xml           ← credits list
  defender.xml          ← defender classes & caps (level, boost, recruit, class)
  defender_skills.xml   ← defender skill trees
  enemy.xml             ← enemy stats & attacks
  enemy_plus.xml        ← same, but for New Game+ enemies
  game_progression.xml  ← triggers, quests, plotlines
  heroes.xml            ← hero character start information
  hotkeys.xml           ← hotkey layouts
  items.xml             ← item definitions (weapons, armor, skulls, etc)
  journal.xml           ← journal layout & entries
  journal_style.xml     ← journal formatting
  locale.xml            ← default locale information
  names.xml             ← name bank for random names (recruits)
  paths.xml             ← default mod & save path information
  recruit.xml           ← starting recruit information
  resolutions.xml       ← supported window resolutions
  spells.xml            ← spell definitions
  stats.xml             ← stat definitions
  tips.xml              ← tips for the "tips & tricks" menu
  
  scenes/scripts.xml        ← cutscene scripts
  scenes/puppet_shows.xml   ← "puppet show" scripts (animated sprites), as seen in DQI ending
  scenes/aliases.xml        ← image & light file aliases (redirect a file to a different one in the cutscene script under various conditions)
```

Next, we'll dig into the various data files and explaining how they work. 
