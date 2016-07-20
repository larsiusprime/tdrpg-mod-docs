##3.1 HD vs Original

The game is split into "HD" art and "original" art.

If you open the `options/pc.xml` file you'll notice this section:

####Sprites & Cutscene option
```xml
<graphics>
	<sprites s="hd" choices="original,hd"/>
	<cutscenes s="hd" choices="original,hd"/>
	<transition_effect b="true"/>
	<highlight_aoe b="false"/>
	<particles f="1.0" range="0,1" step="0.1"/>
</graphics>
```

The "cutscenes" option controls cutscenes & dialogue portraits, and "sprites" controls everything else. If you want to make a mod that only allows pixel art, you should change the file to this:

```xml
<graphics>
	<sprites s="original" choices="original"/>
	<cutscenes s="original" choices="original"/>
</graphics>
```

Or this for only HD art:

```xml
<graphics>
	<sprites s="hd" choices="hd"/>
	<cutscenes s="hd" choices="hd"/>
</graphics>
```

Do note that if you make a pixel-art only game, that many files in the "_hd" folder will still be necessary as many things like buttons and UI chrome always draw from the hd version no matter what option is selected.

####Cutscenes

####Defenders

Defender art can be found in `gfx/_hd/defenders/` and `gfx/_orig/defenders/`. For instance, the berserker class has this structure:

`_orig/defenders/<class_name>/` (original art):
```
     g_head.png        ← generic recruit head icon
     g_icon.png        ← generic recruit icon
     g_icon_big.png    ← generic recruit large icon
     g_sprite.png      ← generic recruit sprite sheet
     h_head.png        ← hero head icon
     h_icon.png        ← hero icon
     h_icon_big.png    ← hero large icon
     h_sprite.png      ← hero sprite sheet
```

`_hd/defenders/<class_name>/` (hd art):
```
  h/                   ← (hero)
     half/               ← half-size assets
       atlas.png           ← half-size texture atlas
       atlas.xml           ← half-size texture atlas metadata
     atlas.png           ← full-size texture atlas
     atlas.xml           ← full-size texture atlas metadata
     head.png           ← hero head icon
     icon.png           ← hero icon
     icon_big.png       ← hero large icon
  g/                   ← (generic recruit)
      head/            ← head folder
        <layers>.png     ← individual layer files
      icon/            ← icon folder
        <layers>.png     ← individual layer files
      icon_big/        ← large icon folder
        <layers>.png     ← individual layer files
      sprite/          ← texture atlas folder
        <layers>.png     ← individual layer files
```

####Enemies

####Effects

####Items

####Spells

####Tiles

####UI

####World Map
