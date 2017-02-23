##2.1 Battle tag

```<battle>``` starts with these three tags:

```xml
<tiles_per_square value="2"/>  <!-- how many individual tiles are in each battle square -->
     <tileset_style value="dq1"/>   <!-- whether we use DQI or DQII tileset format -->
     <casual hp="0.4" atk="0.3"/>   <!-- enemy hitpoint and attack multiplier for casual mode -->
```

Then we have the `<terrain>` sub-tag which has:
```xml
<legal>                         
     <type id="rock"/>            
     <!-- snip -->
     <type id="dull_pavement"/>
</legal>
```

This tag specifies which kinds of tiles are considered “legal” for defenders to stand on. To add new types of legal terrain, just add a line like the one below in between the opening and closing tags for “legal_terrain.”

`<terrain id="yellow_brick_road"/>`

If you add a tileset with a corresponding filename, and then use it in a battle, defenders will be able to stand on it.

The `id` attribute in the tag is a “reference” to a specific tileset. When you reference an id like this somewhere in the data, the game will expect to find a correspondingly named file in a specific location.

In this case, by mentioning "yellow_brick_road" as a legal tileset for defenders to stand on, the game will be looking for a corresponding graphic asset called "tile_yellow_brick_road.png"

If you pop on over to the `gfx\_hd\tiles\` and `gfx\_orig\tiles\` you’ll see a lot of graphics files. This is where the different tilesets you’re referencing are stored. We’ll get back to creating battle maps later, this is just a quick aside to show you how referencing works.

Next you'll see the `<water>` sub-tag:
```xml
<water>
	<type id="water"/>
	<type id="sewage"/>
</water>
```

This just specifies that the "water" tile and the "sewage" tile both count as water for the purposes of swimming enemies.

Then there's the `<path>` sub-tag:

```xml
<path>
	<type id="grey_dirt"/>
	<type id="black_dirt"/>
	<type id="red_dirt"/>
	<type id="black_pavement"/>
</path>
```

These tiles count as "path", the portion of the map that's legal for enemies to walk on, but which defenders can't stand on.

Now we're finished with the `<terrain>` tag. The next sub-tag in `<battle>` is `<interactive>`, and it looks like this:

```xml
<interactive>
	<feature id="crystal_small" type="bomb" x="0.75" y="1.00">
		<owner type="defender" class="mcguffin" handle="mcguffin" skill="crystal" />
		<bomb size="1" base_dmg="10" sfx="crystal_shatter" sfx_splash="small_explosion"/>
		<offset x="0.0" y="0.0"/>
		<terrain value="wall"/>
	</feature>
	<feature id="crystal_medium" type="bomb" x="1.00" y="1.00">
		<owner type="defender" class="mcguffin" handle="mcguffin" skill="crystal" />
		<bomb size="2" base_dmg="10" sfx="crystal_shatter" sfx_splash="medium_explosion"/>
		<offset x="0.0" y="-0.1"/>
		<terrain value="wall"/>
	</feature>
	<feature id="crystal_big" type="bomb" x="1.25" y="1.00">
		<owner type="defender" class="mcguffin" handle="mcguffin" skill="crystal" />
		<bomb size="3" base_dmg="10" sfx="crystal_shatter" sxf_splash="big_explosion"/>
		<offset x="0.0" y="-0.2"/>
		<terrain value="wall"/>
	</feature>
</interactive>
```

This defines various interactive elements that are available in battles. For instance, the "crystal" spell, which we'll get to later, uses the "spawn_interactive" action with these objects as potential targets.

TODO: document all the possibilities here
