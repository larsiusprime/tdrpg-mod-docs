##2.6 Battle rewards

The next tag in index.xml is `<reward_data>`. This is where you specify what rewards the player gets for beating battles on different settings. First off, let’s talk about the various challenge levels. Although they’re displayed in-game as "Casual", "Normal", "Advanced", and "Extreme", internally they are called `casual`, `easy`, `medium`, and `hard`.

This is because the internal names came naturally to us as programmers, but we later wanted to give better signals to players about where they should start, and we were afraid that if the default difficulty setting, “Normal,” were instead displayed as “Easy,” some players would be tempted to skip it right away (and get their butts kicked). That said, the internal references are casual, easy, medium, hard, rather than what you see in-game.

Here’s another place where I’m not always consistent - in some places I use “med” for medium and in others I spell it out as “medium.” Just follow whatever standard I’m using in a given file and location. In most places in the engine I treat “med” and “medium” as synonyms, but I can’t guarantee that.

With that out of the way, let’s look at how these work.

```xml
	<reward pearl_id = "2" diff="easy" win_type="normal" type="progress" value="" />
	<reward pearl_id = "2" diff="easy" win_type="perfect" type="gold" value="100" />
	<reward pearl_id = "2" diff="med" win_type="normal" type="xp" value="75" />
	<reward pearl_id = "2" diff="med" win_type="perfect" type="item" value="weapon_bow_2" />
	<reward pearl_id = "2" diff="hard" win_type="normal" type="xp" value="150" />
	<reward pearl_id = "2" diff="hard" win_type="perfect" type="item" value="weapon_bow_3" />
```

This is the third battle in the game. `diff` means difficulty, or the challenge level, `win_type` is the reward’s particular victory condition and can be either “normal” or “perfect”, `type` means the kind of reward, and `value` is generally a number if xp/gold, or a specific item id if the type is “item.”

You’ll notice there is no entry for “casual.” Casual rewards are automatically generated, and are always half the reward for “easy” (ie, normal). We never reward anything other than gold or xp for “easy” challenges, so rewarding an item for easy challenges will probably cause the casual reward to break because it assumes a numerical reward it can copy and cut in half.

You’ll also notice that the most basic reward, beating the level on “easy” with `win_type` “normal” (ie, just passing without a perfect) will reward “progress” with no value given. This is a special value that technically does nothing by itself, but will display to the user that beating the level will unlock the next location on the map. Actual map progression/unlocking is handled in `game_progression.xml`.

These are the legal values for “type”:

```
type="progress"      ← value ignored
type="xp"            ← value = amount of xp
type="gold"          ← value = amount of money
type="item"          ← value = item type, level, and amount
type="finish"        ← value = cutscene to display
type="finish_puppet" ← value = cutscene + puppet show to display
```

So, progress, xp, and gold are pretty simple to understand. “item” bears a little explaining. The correct format is “<class>_<type>_<level>_<count>”. First is the item’s class. There are four item classes: `weapon`, `armor`, `accessory` and `nonequip` (unequippable items).

Every item is in one of those four classes. Books are classified as accessories and skulls as nonequip.

Next is item type, which is a word like “sword”, “bow”, “skull”, “light” (for light armor), etc. Next is item level, which is just the item’s numerical id. Finally, the last underscore and value is optional and specifies count, or how many copies of the item to give.

So, this would give 3 stone shivs to the player:
`type="item" value="weapon_sword_1_3"`

And this would give 1 Brigandine:
`type="item" value="armor_heavy_10"`

Next, let’s talk about the “finish” and “`finish_puppet`” values you can specify as a reward. This is how you specify an end-of-game cutscene. So, for pearl #36, ie, “The Way Out,” instead of awarding “progress”, just beating the level ends the game with the cutscene “`ending_4_6_outro`.”

```xml
	<reward pearl_id = "36" diff="easy" win_type="normal" type="finish" value="ending_4_6_outro,sad" />
```

For the final battle, the reward is “finish_puppet” which means: don’t just play a cutscene, but also play a puppet show. A “puppet show” is a short animated sequence using sprites. We currently only use this for the final sequence where Zelemir and/or Bakal permanently cross over to the “other side” to confront Eztli-Tenoch. We’ll go into how puppet shows work and are specifically triggered later, for now, just know that in terms of setting a reward it’s basically the same as triggering a cutscene.

What’s more relevant is how to trigger different ones depending on the outcome of the battle. Right now this is set up specifically to deal only with the situation we coded where you have a final battle with a mcguffin (Azra) and an alternate mcguffin (Zelemir).

```xml
		<reward pearl_id = "40" diff="easy" win_type="normal" type="finishpuppet" value="ending_zelemir_unscathed|ending_zelemir_wounded|ending_zelemir_dead|ending_zelemir_unscathed|ending_zelemir_wounded|ending_zelemir_dead" />
		<reward pearl_id = "40" diff="easy" win_type="perfect" type="xp" value="400" />
		<reward pearl_id = "40" diff="med" win_type="normal" type="xp" value="2100" />
		<reward pearl_id = "40" diff="med" win_type="perfect" type="item" value="weapon_bow_9" />
		<reward pearl_id = "40" diff="hard" win_type="normal" type="xp" value="5000" />
		<reward pearl_id = "40" diff="hard" win_type="perfect" type="item" value="weapon_sword_12" />
```
Let’s unpack that a bit:

type="finish_puppet" value="ending_zelemir_unscathed|ending_ze...

At the end we have a really long value string, with six cutscene id’s separated by a vertical pipe character, “|”. These six cutscene id’s are specified in a specific order, and correspond to the six possible outcomes of the final battle. Those outcomes are, in order:

```
A - Perfect++  (Azra unharmed, Zelemir unharmed)
B - Perfect+   (Azra unharmed, Zelemir wounded)
C - Perfect    (Azra unharmed, Zelemir dies)

D - Passed++   (Azra wounded, Zelemir unharmed)
E - Passed+    (Azra wounded, Zelemir wounded)
F - Passed     (Azra wounded, Zelemir dies)
```

You’ll notice that there’s only 3 different cutscenes, and the outcomes for A, B, and C, are respectively also applied to outcomes D, E, and F. So basically, in terms of which cutscene to show, this data setup doesn’t care whether Azra gets wounded or not in terms of which ending you get, the only variable that makes a difference is whether Zelemir is unscathed, is wounded, or dies. We could have very easily made six different unique endings with the above setup, but we felt three was enough.

There’s one other possible ending - game over, which only happens if you lose the final battle. The trigger for showing a cutscene on failure is specified in the level data itself, rather than here (don’t ask me why I did it that way, that’s apparently how it’s set up). We’ll cover that later.

This whole example of showing specific cutscenes in response to specific battle outcomes is a hacked-together special case just for dealing with the final level. Generally speaking, if you just want to show a cutscene after beating a battle, or even responding to whether you got a perfect or just a pass, you would do that through generic game progress triggers in `game_progression.xml`, not through crazy reward parameters. 
