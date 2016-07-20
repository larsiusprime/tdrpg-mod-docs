# tdrpg-mod-docs
Mod documentation for the TDRPG engine (as seen in Defender's Quest)

#0. Finding, Installing, and Playing Mods

[How to find and install a mod.](00.md)

If all you want to do is play a mod, this is the only section you need to read!

#1. Introduction

So, you want to make a mod for Defender’s Quest. This guide will show you how.

There is a [mod editor](https://github.com/Autoquark/dq1-unofficial-mod-editor) in the works, but it's in very early stages.
Until it's finished, you’ll be doing almost everything using simple text and image editors.

If you don’t know what XML is, for instance, I suggest [reading up on that now](https://steamcommunity.com/linkfilter/?url=http://en.wikipedia.org/wiki/XML).

**NOTE:**
*This guide is a work in progress. Many of the sections are stubs and still need to be filled out. Also, mod functionality has not been robustly tested, and might need a few more patches to bring it up to speed. I’ll need some help from adventurous modders to test the limits of the system.*

**SPOILER ALERT:**
*If you’re poking around in the game’s data files, you will come across spoilers! This guide talks about these files in great detail, so it will also contain lots of spoilers. Play the game first if you don’t want to be spoiled!*

  1. [Terminology](01_01_terminology.md)
  2. [Creating your first mod](01_02_first_mod.md)
  3. [File system overview](01_03_overview.md)

#2. Core Data Files and **index.xml**

As you can see from the previous section, there’s a lot of data files! Fortunately, the most important data is in only a few of them. These are the “core” data files, and they’ll be the ones we’ll talk about first.

They are:

```
xml/defender.xml
xml/defender_skills.xml
xml/game_progression.xml
xml/enemy.xml
xml/items.xml
xml/bonus.xml

xml/scenes/scripts.xml
xml/scenes/puppet_shows.xml
maps/index.xml
tables/exp.csv
tables/recruit.csv
tables/<character_class>.csv
```

We’ll start with `index.xml`, the file that ties most of the game’s systems together.

  1. [Index.xml](02_01_00_index.md)
    * [Battle tag](02_01_01_battle.md)
    * [Overworld tag](02_01_02_overworld.md)
  2. [Overworld features](02_02_overworld.md)
  3. [Map pearls](02_03_map_pearls.md)
  4. [Towns](02_04_towns.md)
  5. [Battle rewards](02_05_battle_rewards.md)
  6. [Tutorial levels & NewGame+ Rewards](02_06_tutorial.md)

#3. Graphic

  1. HD vs Original
  2. Layered vs. Baked HD sprites
  3. Pipeline

#4. Defender Data

  1. Class definitions
  2. Graphics
  3. Character colors
  4. Skills
  5. Damage flavors
  6. Attack skills, "Techniques", part 1
  7. Attack skills, "Techniques", part 2
  8. Passive skills, "Traits"
  9. Mcguffin's skills, Spells

#5. Battles

  1. Layered battle setup

#6. Cutscenes

  1. Standard cutscenes
  2. "Puppet shows"

#7. Game progress & triggers

#8. Enemies

#9. Items
