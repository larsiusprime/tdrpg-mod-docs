##2.5 Towns

You can usually buy weapons, armor, recruit characters, and trigger sidequests from towns. Here’s an example of a typical town:

```xml
<town id="monastery" name="$INDEX_MONASTERY_TITLE">
	<background value="monastery_inside"/>
	<shop item_class="weapon" type="sword" lvl="2,3,5" plus_lvl="21,22,23" />
	<shop item_class="weapon" type="bow" lvl="1,2,4" plus_lvl="18,19,20"/>
	<shop item_class="weapon" type="staff" lvl="1,2,4" plus_lvl="20,21,22"/>
	<shop item_class="armor" type="light" lvl="1,2,4" plus_lvl="22,23,24"/>
	<recruit type="berserker"/>
	<recruit type="ranger"/>
	<recruit type="healer"/>
	<talk value="sidequest_2_get"/>
</town>
```

This is the entry for the monastery. The `id` attribute is the string id for the town (used to reference it throughout the game), and the `name` attribute is what’s displayed to the player on the town screen.

Inside the opening and closing tags for the town, there are various sub-tags.

####Equipment for Sale

First, there’s a list of shop tags, one for each type of weapon offered.

```xml
<shop item_class="weapon" type="sword" lvl="2,3,5" plus_lvl="21,22,23" />
<shop item_class="weapon" type="bow" lvl="1,2,4" plus_lvl="18,19,20"/>
<shop item_class="weapon" type="staff" lvl="1,2,4" plus_lvl="20,21,22"/>
```

This town sells swords, specifically swords level 2, 3, and 5, which you can look up in `items.xml` - these are “Metal Shiv”, “Rusty Sword”, and “Iron Sword”, respectively. The `lvl` attribute specifies which items are available in the normal game, and `plus_lvl` indicates what’s for sale in NG+. (An item’s “level” is simply a unique numerical id). If no shop tags for the item_class "weapon" are found, the town will not show the “weapons” button.

Prices are set in `items.xml`, and are always the same for every town, since the price is tied to the item, not the store. Armor (as well as any other item class) is handled exactly like weapons, except you use "armor" for the item_class instead.

Next, let’s talk about recruits.

```xml
<recruit type="berserker"/>
<recruit type="ranger"/>
<recruit type="healer"/>
```

These tags are pretty self explanatory - they simply mention which defender classes can be recruited here. If none are found, the town will not show the “recruit” button.

Next, we have the “talk” tag:

```xml
<talk value="sidequest_2_get"/>
```

All this does is specify the string id of a cutscene (defined in cutscenes/scripts.xml) to play when the button is pressed. Cutscenes are one of the many events that can set off a trigger, and in `game_progression.xml` we’ve set it up so that watching one of these cutscenes will unlock the corresponding sidequest on the map. We’ll show you how to do that later.

Just setting up the talk tag is not enough to make the talk button appear in a town, because it is disabled by default. You must also specify a trigger through `game_progression.xml` that “unlocks” the town cutscene. In the default campaign, we use this to make these town cutscenes only appear in NG+ mode, and often only after you’ve visited a town for the first time.

We’ll talk more about this when we get to progress and plot triggers.

####Backgrounds

By default, towns will look for an art file that matches their string id in the cutscenes/backgrounds/ folder, with the prefix “back_”. So the town with the string id “ghost_town” will look for a background file named “back_ghost_town.png” You can also specify a specific file if you want, however:

```xml
<town id="hermit_1" name="$INDEX_HERMIT_1_TITLE">
		<background value="river_1"/>
		<!--snip-->
</town>
```

####Special Case 1: Treasure Chamber and Evni

Next, we had a specific situation in the Treasure Chamber with the special sword, “Evni.” This is one of only two unique items that is ever sold in a store (you can set an item as unique in data_items.xml). When an item in a store is “unique,” it will not show up for sale if it detects that you already have it in your inventory. However, in NG+ you can upgrade Evni, which just deletes the old Evni and replaces it with Evni+ -- which is actually a different item as far as the game engine is concerned. So it used possible to buy Evni, upgrade it to Evni+, then go back and buy Evni again!

To fix this, we added the following tag to the treasure chamber:

```xml
<town id="treasure_chamber" name="$INDEX_TREASURE_CHAMBER_TITLE">
	<!--snip-->
	<shop item_class="weapon" type="sword" lvl="9,11,13" plus_lvl="25,26,13">
		<dont_show value="13" if_have="19"/>
	</shop>
	<!--snip-->
</town>
```

This extra tag will not show sword #13 (Evni) if you currently own sword #19 (Evni+). For those of you less experienced with XML, note that the `<shop>` tag has been split into an opening and closing tag. If you are not adding children to a tag, you usually end it with a `/>` rather than a `>`.

The following examples are equivalent:

```xml
<shop item_class="weapon" attribute="blah" thing="whatever"/>
```
(open and close the tag on one line)

```xml
<shop item_class="weapon" attribute="blah" thing="whatever">
</weapon>
```
(open and close the tag in two lines)

However, the second example lets you add child tags, such as `<dont_show/>`, which we’ve done above.

####Special Case 2: Hermits and Upgrades

Here’s an example of one of the “Hermit” towns in NG+, where you can upgrade unique items for better ones.

```xml
		<town id="hermit_1" name="$INDEX_HERMIT_1_TITLE">
			<background value="river_1"/>
			<shop item_class="weapon" type="sword" upgrade="true" lvl="4,6,8,10,12,13" plus_lvl="4,6,8,10,12,13" replace="14,15,16,17,18,19"/>
			<shop item_class="weapon" type="bow" upgrade="true" lvl="3,5,7,9,11" plus_lvl="3,5,7,9,11" replace="13,14,15,16,17" />
			<shop item_class="weapon" type="staff" upgrade="true" lvl="3,5,7,9,11,13" plus_lvl="3,5,7,9,11,13" replace="14,15,16,17,18,19" />
			<shop item_class="armor" type="light" upgrade="true" lvl="3,5,7,9,11,13,14" plus_lvl="3,5,7,9,11,13,14" replace="15,16,17,18,19,20,21" />
			<shop item_class="armor" type="heavy" upgrade="true" lvl="3,5,7,9,11,13,14" plus_lvl="3,5,7,9,11,13,14" replace="15,16,17,18,19,20,21" />
		</town>
```

I believe all the hermit towns in NG+ are identical except for backgrounds. What’s special here is that we have two new attributes: `upgrade` and `replace`.

If upgrade is set to “true”, then the store instead becomes an upgrade shop rather than a normal store. Rather than looking for the lvl tag to see what’s for sale, it interprets the content of the lvl tag as items that it can upgrade for you. Since hermit towns only show up in NG+ for the default campaign, we of course use plus_lvl in this case. (Theoretically you could put upgrade shops in a normal mode game, though I’ve never tested that).

So, if you have any of the swords with a level equal to 4,6,8,10,12, or 13 (all the unique swords in data_items.xml), they will show up in the store. It will only show the items on the list that are actually in your inventory. In the default campaign, upgrades cost skulls, but this is handled in data_items.xml rather than here- we just fiddle with the price settings for the upgraded versions of the items. And as you can guess, the “replace” attribute specifies which items the store will offer as upgrades for the original list. The order of both lists matter!

```xml
<shop item_class="weapon" type="sword" upgrade="true" lvl="4,6,8,10,12,13" plus_lvl="4,6,8,10,12,13" replace="14,15,16,17,18,19"/>
```

This means that sword 4 becomes sword 14, 6 becomes 15, 8 becomes 10, etc. We’ve set things up so that 4 is Blood-Feud Kopal and 14 is Blood-Feud Kopal+, etc, so it feels like you’re “upgrading” the item.

Technically speaking, you could just use this as a way to swap one item for a completely different one, and use scrap instead of skulls, but again, we’ve never tested using the system in that way. Also, I’m not sure if this system will work with non-unique items, there might be some code in the engine that specifically expects things to be unique.

####Special Case 3: Strange Monument

TODO
