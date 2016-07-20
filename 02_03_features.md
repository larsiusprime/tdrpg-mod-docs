##2.2 Overworld features

The next tag is `<features>`. This is a collection of specific art pieces that are placed around the overworld, and is used for things like towns, the cliffs surrounding the pit, the coliseum, the desert fortress, etc.

Here’s an example:
```xml
<feature shown="true" id="pitwalls_nw" _x="0" _y="0"/>
```

This defines a feature, with the id of "pitwalls_nw" at location (0,0) - the top-left corner of the map, and makes it visible ("shown") by default. The game will look for a corresponding piece of art, `feature_pitwalls_nw.png`, in the `gfx/_orig/tiles` folder, when it tries to draw the overworld.

*TODO: verify this next part:*
In HD art mode, the positions given in these tags are ignored, as the placements are defined in the `tiled/overworld/map.tmx` file. IIRC, the engine still uses the index.xml definitions to define other properties for these features, however.

Features can be modified by game triggers - specifically, their visibility can be changed. For instance, the town of Karsk is burned to the ground early in the game. This is accomplished by starting the game with two different versions of the town’s graphic feature, one visible, and one invisibile.

```xml
<feature shown="true" id="karsk@a" _x="165" _y="520" atlas="a"/>
<feature shown="false" id="karsk_explode@a" _x="165" _y="520" atlas="a"/>
```

After Karsk is burned in the story, its associated map pearl is disabled, the first feature is hidden, and the second one is shown. We’ll get into how to do that when we cover map triggers.

You’ll notice that there is an “@a” appended to both of the above id’s. If you just want to place a feature down somewhere, you just give it the same id as the graphic you want to show (without the “feature_” prefix), so in this case, you could just have written id="karsk".

However, if you need to target that feature with a game trigger later on, you’ll want to give it a suffix starting with “@.” This is because you might have multiple features of the same basic graphic id, and you need to differentiate between which one you want to target. The “@” symbol is used as a separator between the id and suffix in this case.

I think you can use just about anything as the suffix, but I would stick to single-character lowercase latin letters just to be safe.

The `atlas="a"` bit tells the game to auto-generate a texture atlas for this feature. All features with the same atlas value will be drawn to the same atlas. The max size for a texture atlas is 1024x1024, so bigger features should go on a separate atlas.

By default, features will be drawn above tileset terrain but below "map pearls" (the shiny red, blue, purple, and yellow spheres that specify locations) as well as the small white dots that connect them. If you want to draw a feature above these things, set the `over` attribute to "true."

```xml
		<feature shown="true" id="mountain_gate@a" _x="553" _y="318" over="true" atlas="a" immutable="true"/>
```

This draws the stairs and gate for the monastery above the connecting map dots.

The "immutable" tag signifies that this feature will never be changed in any way, so it doesn't matter what values a trigger has tried to set for it.

**NOTE:**
For boolean values in data files to work correctly, make sure you ALWAYS do it like this:
```<tag boolean="true"/>```

Ie, all lowercase, one word, spelled out as "true."
Never use "TRUE", "True", "trUe", or "1". None of those will work.
Also, for any boolean attribute in an XML tag, if you don’t specify a value, it will be the same as setting it to false.

So this:
```xml
<feature shown="true" id="mountain_gate@A" _x="533" _y="318"/>
```

Is exactly the same as this:
```xml
<feature shown="true" id="mountain_gate@A" _x="533" _y="318" over="false"/>
```

Finally, sometimes you want to draw a feature that is sometimes visible and sometimes not depending on where the user is on the map. This is a great way to make ceilings for caves and large buildings - we use this for the desert fortress, for instance. Here’s how you do it:

```xml
<feature shown="true" id="fortress_roof@a" _x="643" _y="149" touch_hide="true" show_range="15-28,48,49,50,54"/>
```

Setting `touch_hide` to "true" means that when the map marker (Azra’s overworld sprite) is at a certain location, the feature will be shown, and when it’s somewhere else, the feature will be hidden. You enter data for “show_range” the same way you specify a range of pages to be printed on a printer, using numbers separated by commas and dashes.

The above example will show the feature when Azra is on any pearls between 15 and 28, as well as 48, 49, 50, and 54. These happen to be all of the pearls inside of the desert fortress, so the user sees the ceiling disappear when they go "inside" and re-appear when they leave.

The high-numbered pearls added to the end are the sidequests and special locations that were added in the New Game+ expansion, after #’s 29-47 had already been defined for other purposes outside of the fortress. We’ll touch more on this when we get to game_progress.xml and triggers.
