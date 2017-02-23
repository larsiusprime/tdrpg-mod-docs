##4.1 Class Definitions

The normal game has these classes:

* Mcguffin
* Berserker
* Ranger
* Healer
* Ice Mage
* Knight
* Dragon
* Sorceror
* AntiMcguffin

The Sorceror class is for Zelemir, and the AntiMcguffin class is for Tletl-Meztli. Note that Zelemir shows up as both an enemy and a defender, and has both defender and enemy definitions.

I'm going to skip ahead and look at the entry for the berserker because it is simpler than the Mcguffin. Don't worry, we'll pop right back to the Mcguffin.

```xml
	<class_entry id="berserker" name="$CLASS_BERSERKER">
		<culture id="ash"/>
		<graphic id="berserker"/>
		<cost value="25"/>
		<sex default="male"/>
		
		<item slot="1" class="weapon" type="sword"/>
		<item slot="2" class="armor" type="none"/>
		
		<range max="1.80" min="0" shape="circle" type="Melee" />
		<attack value="sword_strike"/>
		<blurb txt="$BLURB_BERSERKER"/>
	</class_entry>
```

The "id" value is very important. This is the universal string handle by which you'll refer to Berserkers throughout the game. This has nothing to do with the displayed name, which is specified under "name."

####Note:
You'll notice that "$CLASS_BERSERKER" looks like some weird code thing rather than the word "Berserker", which is how it appears in game. That's because this is a [localization flag](https://github.com/larsiusprime/tdrpg-mod-docs/blob/master/01_03_localization.md).

The culture tag I believe is ignored, part of some discarded feature we never wound up using.

The graphic id is very important - this string associates this class with a graphic definition which is supplied elsewhere (see the graphics section).

The cost value I believe is ignored, I should remove that sometime. The game looks up the summon/boost costs for each defender from the data tables.

The sex id is ignored, we might eventually add support to recruit male/female variants of any class for modders who choose to add that content, but it's just leftover cruft for now.

The item values specify what kind of items this class can equip. You need to specify an item class and an item type for each item slot. The default is 2 slots, but in theory you can provide an arbitrary amount of slots, though this has not been tested and the user interface layouts would have to be updated to accomodate this change, too. One major difference between DQDX and DG legacy is that DQDX doesn't assume each character has exactly 1 weapon slot and exactly 1 armor slot -- so you can easily mod a character to have two different weapons of the same slot if you like.

For the range tag, you can specify minimum & maximum range distance. Generally you want the minimum value to be "0" except for when you want a dead zone inside, like rangers have.

You can also specify shape, the legal values are:

  ```
  "circle"        ← standard circular range. If min is not 0, will have a dead zone.
  "box"           ← square range. If min is not 0, I don't think it will create a dead zone.
  "double_circle" ← dual range, like dragons use. Min range specifies boundary
  ```

The "type" value I think is just for display purposes in the character class overviews in the interface. The legal values are "ranged", "melee", and "ultimate", and I don't think case matters. I *think* all it does is append "$TYPE_" to the front, and then show the localized text. So I think you could specify your own types, but you'd have to create corresponding localization entries.

The attack tag is definitely ignored. Why is that even still in there? Game design is messy :P

The blurb specifies the text that you see in the recruit screen, as well as various other places where it describes the class. Again, this is localized.

Now, let's go back to the mcguffin.

```xml
<class_entry id="mcguffin" name="$CLASS_MCGUFFIN">
	<type value="mcguffin"/>
	<boost value="false" show_bars="false"/>
	<culture id="ash"/>
	<graphic id="mcguffin"/>
	<cost value="0"/>
	<sex default="female"/>
	
	<item slot="1" class="accessory" type="book"/>
	<item slot="2" class="accessory" type="book"/>
	
	<range max="0" min="0" shape="circle" type="Ranged" />
		
</class_entry>
```

The mcguffin has some extra stuff. First of all, in the equip section you'll see there's neither armor or weapon, but instead two accessory slots which both take a "book."

You'll also notice a `<boost>` tag with `value` set to "false" and `show_bars` also set to false. This means this character is unboostable in battle by default, and no attack skill cooldown bars will show up in their selection preview either.
