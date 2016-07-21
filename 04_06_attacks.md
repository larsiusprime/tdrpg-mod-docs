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
  "guided_melee"         - basic melee attack (there is no "unguided_melee")
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
