##2.4 Map pearls

“Map pearls” represent locations on the overworld that you can visit. All of the pearls are listed in the `<pearl_data>` tag.

Here’s an example:
```xml
<pearl id="0" level="$INDEX_1_1_WHERE_AM_I_TITLE" level_id="1_1_where_am_i" description="$INDEX_1_1_WHERE_AM_I_TEXT" _x="70" _y="90" _type="battle"/>
```

Let’s spell out the relevant attributes:

```
id="0"                                   ← numerical id, reference
level="$INDEX_1_1_WHERE_AM_I_TITLE"      ← title displayed to player (resolves to "The Half-Way World")
level_id="1_1_where_am_i"                ← string id, reference
description="$INDEX_1_1_WHERE_AM_I_TEXT" ← description displayed to player (resolves to "Lost and alone...")
_x="7"                                   ← x coordinate on map (base 600)
_y="90"                                  ← y coordinate on map (base 600)
_type="battle"                           ← whether this is a battle, town, sidequest, etc.
```

####NOTE:
You’ll notice that the x, y, and type attributes all have a leading underscore, "_". Don’t leave this off! It’s required for map pearls.

I’m unfortunately not very consistent about this. In other places you’ll find x/y attributes without the underscore - but whatever format I’m using in a given place, you should follow the same, as that’s what the game will expect.

The reason I used an underscore is that there are a lot of variables in the game called "x" "y" and "type", and I wanted to avoid tripping up against those reserved keywords in the code when I accessed them from the XML. On second thought this probably just made thing more confusing, but the game engine expects it now, so there you go.

###Referencing Levels

There are two ways that levels get referenced - by numerical id, and by string id. The first level’s numerical id is 0 (zero), and it’s string id is "1_1_where_am_i." Both of these will be used in different locations to refer back to this pearl. For instance, the "touch_hide" attribute of overworld features that you read about in the previous section uses numerical id’s to specify specific map pearls.

The string id can be anything, as long as it’s unique and you use it throughout the game. Originally, the string id’s were supposed to describe the act and "scene" of the level, as well as its title, but over the course of development we changed the number of acts from 4 to 7, and changed many of the titles.

However, by that point we already had a bunch of other data file hooked up already and referencing the old string id’s, so it wasn’t worth the risk of changing everything. So that’s why levels in act 7 are named things like "4_1_blah_blah" and the last level is "12_4_final" (we didn’t originally know how many acts we would have, so when I created the final level way in advance I put in the far-flung act "12" scene "4" - way more than we would need. Again, confusing, I know.)

Okay, whatever. On to explaining things.

###Pearl Settings

There are several kinds of pearls you can put on the map. Here are the legal values for "_type:"

```
"battle"        ← A normal battle. Default color is red.
"place"         ← A non-battle location. Usually means “town.” Default color is blue.
"sidequest"     ← Special battle type. Default color is purple.
```

There are some extra optional attributes you can specify, too:

```
button_text="$MAP_TEXT_PRISON"
sub_type="upgrade"
optional="true"
suppressed="true"
```

`button_text` lets you specify exactly what goes on the button. The default for battles is “BATTLE” and the default for towns is “TOWN.” Sometimes, you might have a “town” location that’s not really a town in terms of story, such as Ozimal’s prison or the Dragon’s lair. This is how you specify an alternate name.

`sub_type` is currently only used for the hermits in NG+. The only value it recognizes is “upgrade” and this value turnsthe pearl gold instead of blue.

`optional` is used to flag a battle as not required to beat the game. This way, NG+ will be unlocked even if you never play this battle. We only use this for “The Way Out” in the default campaign.

`suppressed` keeps a pearl from showing up on the map, even if it’s been unlocked in game progress, etc. We use this to temporarily hide a feature we’re not quite finished with yet that we can release later, but still have the triggers for it work correctly. When we remove the suppression the location will automatically appear in save files that have fulfilled the requirements for showing it. I doubt you’ll ever have to use this.

Now, just setting up all your pearls in the index file will not make them appear on the map. By default, all pearls are invisible and none of them are connected to one another. Triggers in `data_game_progression.xml` will do all of the work of making pearls appear as you beat battles, which we’ll get to in a minute.

The next few sections, `<battle_screen_data>`, `<overworld_data>`, and `<party_screen_data>`, contain tutorials that show up in those various screens. We’ll skip those sections for now and come back to them later, when we cover tutorials in general. For now, scroll down to the `<town_data>` tag. 
