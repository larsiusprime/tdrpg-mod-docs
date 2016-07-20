
##2.2 Overworld Tag

The overworld tag is pretty simple:

```xml
  <overworld width="3986" height="2600"/>
```

It simply specifies the total scrollable area of the overworld. The values are given in base-600 pixels, which means that as your overworld scales in size above the smallest vertical resolution (600), these values will scale proportionately as well.

The `tiles` tag is only used in "original art" mode, and defines tile layers for the overworld:
```xml
   <tiles default="dirt">
	<tile rgb="0x808000" value="sand" layer="1"/>
	<tile rgb="0x008000" value="grass" layer="2"/>
	<tile rgb="0x0000FF" value="water" layer="3"/>
	<tile rgb="0xc4c4c4" value="black_stone" layer="4"/>
	<tile rgb="0xFFFF00" value="creep" layer="5"/>
	<tile rgb="0x00FF00" value="sewage" layer="6"/>
   </tiles>
```

**NOTE:** *The following method is ONLY used in original art mode. A totally different method is used to draw the HD overworld!*

These are the tilesets used for the overworld. The default="dirt" attribute in the opening tag specifies what the bottom-most tileset is.

Within the `<tiles>` tag are a list of `<tile>` tags (no 's'). Each of these specifies a pixel color in hexadecimal format (rgb), a tile id (value) and a layer number (layer). So, in this example, the overworld has a `dirt` layer on the bottom, then `sand`, then `grass`, then `water`, then `black_stone`, then `creep`, then `sewage`. All of the tilesets for these layers can be found in `gfx\_orig\tiles\`, but unlike normal battle tiles they start with the prefix "`tile_overworld_`" instead of just "`tile_`." So the overworld grass tile will be "`tile_overworld_grass.png.`"

The overworld is created by looking up several image maps and turning them into tile layers. These image maps are stored in the `maps/` folder, and have the format `overworld_<tile_id>.png`

So if you go to that folder, you should find files like `overworld_sand.png`, which specifies where all the sand is. The game will look for pixels that match the value in the corresponding `<tile>` tag, so for sand, it’s a kind of dark yellow (`0x808000`). Any other pixel value in that file is treated as empty space.

When designing the overworld, I usually have one master .psd file setup with each tileset as a separate layer, each set to "lighter color" so that the pixel color shows through and the black becomes transparent. This way I can see how the layers will look stacked together. When I’m done, I save each layer as a separate png. 
