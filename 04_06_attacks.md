##4.6 Attack Skills, "Techniques"

Attack skills, or "techniques", are the abilities your characters use in battle, and are tied to specific boost levels.

The best way to understand these is to look at how the skills work in the normal game, and then
compare that to their definitions in `defender_skills.xml`. These are heavily data driven, 
so you can do all kinds of crazy stuff here.

There are a few basic components to a technique definition:

```
  info tag       - specifies all the basic properties
  stats table    - specifies stats and properties that change with skill levels
  graphic info   - specifies how the attack looks
  effects        - (optional) if it has any sort of effect (usually just for AOE/Splash projectiles)
  flavors        - (optional) if it has any default flavors
```

####<info>
This tag specifies almost all the relevant information for a skill, and unlike the other tags it's not super self-documenting,
as just looking at the data files doesn't give you a full picture of everything it can do. 
This is probably the most important part of technique documentation.

Here are the most important attributes you can specify in the `<info>` tag. There are others, 
but they only work when using certain types so we'll discuss them then.

**NOTE:** *If an attribute is not present in the info tag, it's the same as it being present with the value "false"*

```
    anim           - the id of the animation that plays when this attack is used
                     NOTE: put ":repeat" at the end of the animation to repeat the same animation for each attack
    sfx            - the id of the sound effect* played when this attack is used
    sfx_each       - if the skill has more than one attack, play this sfx for each attack instead of the normal sfx. This is timed to the "sweet" frames, if any.
    splash_sfx     - if a splash attack, the sound effect to play when the splash damage effect is created. Not sure if this is actually used.
    sfx_end        - the sfx to play for the last attack used. Not sure if this is used?
    heal           - "minor" or "major". If present, makes the attack a heal technique and minor/major drives what effect to play on healed targets.
    type           - the skill's basic archetype. See more below.
    speed          - how fast the attack's collision projectile moves
    shape          - I'm not sure if this is actually even used
    priority       - if multiple techs are available, highest priority is used first.
    single_target  - true:all attacks apply to ONE target. false:spread attacks out over multiple targets
    hitall         - true:each attack hits EVERYTHING in range. false: each attack hits only one enemy.
    random_targets - not sure if this is used?
    strike_through - supposed to make attack pierce through multiple targets. 
                     Not sure it's used, the preferred way to do this now is to add a "strike_through" flavor.
    counter        - if true, works as a counter-attack. Attack will launch in response to a melee attack, which is immediately dodged, and triggers this attack.
    retarget       - true:attack will find a new target if the original one dies while en route.
    orthogonal     - true:makes the projectile "straighten out" along major axis lines. Useful for piercing attacks
```

*See the audio section for how to play multiple random variants of the same basic sound effect

"type" is the single most important attribute specified above. This lets you specify the attack's basic archetype, such as ' type="guided_projectile" '.

Legal technique types:

```
  "spell"                - the skill is a mcguffin spell
  "melee"                - melee attack
  "guided_projectile"    - basic projectile attack, has "homing"
  "spread_projectile"    - spreads out multiple shots in one burst, no homing
  "unguided_projectile"  - unguided projectile, no homing
  "heal_attack_all"      - heals all friends in range, hurts all enemies in range (ie, Zeal)
  "splash_projectile"    - a projectile that does splash damage, like dragon's "fireball"
```

####Melee Attacks
All melee attacks use the "melee" type. Basically, any targeted enemy in the character's range (or melee range if they have dual-range) will be hit by a melee attack as soon as it is fired.

If you want to hit one target multiple times, specify `single_target="true"` and set `num_attacks` in the stats table to a value higher than one. If you want to spread several attacks out over multiple targets, `use single_target="false"` with multiple num_attacks. Specifying `hitall="true"` will basically give you an AOE melee attack.

####Projectiles
Projectiles come in three varieties - guided, unguided, and spread. If guided or unguided, multiple attacks will result in multiple projectiles, and single_target=true/false will determine whether that all goes to one enemy or fired around more generously. Giving this attack a "strike_through" flavor will let it pierce a number of targets up to the "amount" value. Using "spread_projectile" as the type will fire a number of shots equal to the number of attacks, all at once.

####Splash attacks (AOE)
Splash attacks are a bit of a misnomer, and can be confused with splash projectiles. In truth, "splash" by itself means an AOE attack. I'm not 100% sure on this, but I think the "splash" type makes it automatically just hit everything in melee range. So any values for hitall and single_target should be ignored.

The exception is if you set a value for the heal attribute. If you set heal="minor" or "major" it will make this a healing skill, and single_target="true" will make it a single-target heal tech, like aid. Setting single_target="false" and hitall="true" will make it heal everyone in range, like "group_heal."

####Splash projectiles
These are guided projectiles that explode on contact with splash damage. The splash damage is specified in the stats table, and note that any flavors applied to the main skill will be moved to the splash effect, so all enemies affected by the splash will be hit with that flavor.

####Heal/Attack All
This is a special case, only used for Zeal. It's basically an AOE attack that heals all friends in range and harms all enemies in range. 

-------------

####Stats Table
The stats table is much like the `<info>` tag, letting you specify a bunch of attributes, including optional ones, for your technique. However, these let you specify stats that change in value as the technique has more skill points assigned to it.

I think the number of points the player can put into a skill is entirely determined by how many stats entries you create, but I haven't tested that robustly.

Here are the basic attributes you can specify in the stats table.

```
  level          = what skill level this stat definition is for. (0 means you don't have the skill, so 1 is minimum)
  attack_mult    = damage is calculated as (attack_mult * final_attack_stat), and the final attack stat does include item,
                   buff, and boost bonuses. So a value of 0.10 means the tech does 10% of your attack stat, 1.0 means 100% of
                   your attack stat, etc. If this is a heal technique, this is how much HP is restored instead.
  dmg_mult       = only used for "heal_attack_all" type attacks. Since attack_mult is reinterpreted as healing amount for heal
                   attacks, you need to also specify the damage dealt to enemies. dmg_mult takes this role in this special 
                   case.
  cooldown       = how many seconds it takes for the attack to cool down. The character's speed and boost stat will modify 
                   this base value.
  num_attacks    = how many hits this attack can dish out. This gets interpreted in various ways depending on the values of 
                   single_target, hitall, and the type of the attack.
  <flav>_amount  = modifies a default flavor's amount value. "<flav>" represents the flavor id, so in practice you'd see 
                   "stun_amount" or "chill_amount", etc.
  <flav>_time    = same, but the time value
  <flav>_rate    = same, but the rate value
  splash_mult    = what % of the attack's final damage is dealt as splash damage to surrounding targets
  radius         = size of the splash damage radius, or the AOE radius.
```

####Flavors
You can specify a default flavor for the attack by putting a `<flavor>` tag down. "type" will define its id, and amount/time/rate values should also be given. If you don't specify any flavor values in the stats table, these values will always apply to the attack, regardless of skill level. If values are specified in the stats table, those will be used instead.

####Graphics
The `<graphic>` tag is usually for specifying a projectile image for projectile attacks.

Here's the ranger's arrow:
```xml
<graphic id="arrow" rotations="36" width="24" height="24" off_x="0" off_y="0" frames="1" framerate="0"/>
```

This format provides all the information necessary right here. The file id references "gfx/_hd/effects/arrow.png" in _hd art mode and "gfx/_orig/effects/arrow.png" in original art mode. Specifying `rotations` will automatically generate rotated frames for the image -- "4" will only make it round to the nearest cardinal directions, "8" will let it rotate at 45 degree increments, etc. "width" and "height" are the width/height of the original art asset -- it just applies a 3x multiplier to get the size of the hd version.

I'll mention this in the effects section, but to make sure it's not missed here:

**All art in the "_hd/effects" folder is exactly 3x the size of art in the "_orig/effects" folder!** This is a rare place that breaks the general convention where all hd art is exactly twice the size of the original art.

Now, here's the ice mage's ice ball:
```xml
<graphic use_effect="true" id="ice_ball" width="24" height="24" off_x="0" off_y="0" frames="3" framerate="8"/>
```

In this case we're not just making a direct link to an art asset, we're referencing an actual effect (see the effects section). This will allow us to have an animated projectile.

Projectile graphics will usually call for some additional tags:
This lets you specify the animation loop:

*TODO: is this actually used in DQDX if you set use_effect="true" ?*

```xml
<graphic_anim>
  <frame value="0"/>
  <frame value="1"/>
  <frame value="2"/>
  <frame value="1"/>
</graphic_anim>
```

**NOTE:** *you can have an animated projectile, or one that rotates, but NOT both.* 
*TODO: is this above note still true in DQDX?*

You can also specify some positioning so that the projectile appears from the correct location:
```xml
			<graphic_pos>
				<zoff  x="0"      y="1.0"/>
				<left  x="-0.75"  y="-0.3"/>
				<right x="0.625"  y="-0.3"/>
				<up    x="0.225"  y="0.50"/>
				<down  x="-0.225" y="-0.2"/>
			</graphic_pos>
```

The left/right/up/down tags should be pretty obvious - offsets for where the projectile should appear based on the character's animation facing. The unit values are the size of one battle square.

Now what is zoff? Well, it lets you mess with stacking. All objects on screen have x and y positions, and a derived z position which is : (y * screen_width + x). The "z" position is used to calculate which enemy goes in front of another, and higher z wins. zoff lets you add adjustments to how their z offset is calculated, so you can properly position a projectile AND make sure it stacks correctly.

Note that splash and AOE will need a splash effect animation. You specify those like this:
```xml
			<effects time="0.5">
				<effect id="explode_big" chance="1"/> 
				<effect id="explode_medium" chance="1"/>
				<effect id="explode_small_long" chance="1"/> 
				<effect id="explode_small" chance="1"/> 
				<effect id="explode_tiny" chance="1"/> 
			</effects>
```

The time attribute specifies how long the effect lasts, and each `<effect>` tag specifies an effect animation that is part of the splash effect. These all correspond to ids for effects defined in `entities/effects.xml`. You can specify a "chance" value for each one which defines the random weights assigned to each one. The values are all totaled and then normalized, so in the above example each one has a 20% chance of appearing. If you want to shift things towards "explode_big", you could set that weight to 2, or keep it at 1 and lower the other weights.
