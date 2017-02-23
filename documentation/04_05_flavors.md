##4.5 Damage Flavors

One of the central features of the Defender’s Quest battle system is the concept of a damage “flavor.”
Simply put, a flavor is some kind of quality associated with damage that does something interesting.
The “something” depends on the flavor. For instance, when a creature takes damage from an attack that also
has a poison flavor, they will get the “poison” status effect and start taking damage over time.

Some damage flavors don’t normally do anything by themselves, and are only there to categorize the source 
of the damage, such as “physical,” or “magic.” This is so things like special armor can respond to specific 
kinds of attacks, etc.

Damage flavors can have various properties, specifically:

```
    flavor    (the string id of the flavor, ie, “poison”)
    amount    (some number, interpretation depends on flavor)
    time      (number of seconds it will last)
    rate      (value between 0-1, chance of it occurring)
```

So, you could have something like this:

```
  flavor=poison
  amount=0.5
  time=10
  rate=0.75
```

When this flavor is applied to an attack, there is a 75% chance that the victim will take 50% of the attack’s
original damage every second for 10 seconds. Since flavors can have wildly different effects, the exact interpretation 
of the various parameters often varies wildly as well. Often many of the attributes have no meaning for a certain flavor 
(such as “time” for things like “armor_break”) and are just ignored.

Here is a full list of damage flavors and what they do:

####burn
Damage over time. Just like poison except it mutually cancels with chill/freeze, and is removed if an enemy walks into water.
`amt=0.25,t=10,rate=0.75` means: 75% chance of “Deal 25% of original damage every second for 10 seconds.”

####poison
Damage over time. see above

####ever_poison
Just like poison, but always lasts forever. Ignores time value. Not used in game

####bleed
Multiplies damage of incoming attacks. `amt=0.25` means: “Damage taken multiplier becomes 125%”

####ever_bleed
Bleed that lasts forever.

####blinded
Target gets “blind” status, with a reduced chance of hitting their targets. `amt=0.75` means:
“Blinded victim’s chance to hit = 75%”

####disease
Target can’t regenerate while diseased.

####inspire	
Target gets “inspired” status, dealing additional damage with every hit. 
**NOTE:** *This flavor only goes on “healing” attacks that healers target defenders with.*
`amt=1.10` means “Damage given multiplier is 110%”

####inspired_hit
This flavor is automatically applied to the attacks by defenders who are currently “inspired.” 
Behaves very much like a critical hit. 
The status effect sets the rate for this flavor to 1.0. `amt=1.10 means` “Damage given multiplier is 110%” time = ignored

####stun
Target can’t move. Exactly like freeze, except nothing cancels it. `amt` is ignored, `time` = duration

####single_stun
Exactly like stun, but can only be applied to a given target once per battle.

####chill
Slows a target by a specified amount. Canceled by burn.
`amt=0.4` means “Target’s speed becomes 60% of normal”

####slow
Slows a target. Just like chill, except nothing cancels it.

####freeze
Exactly like stun, except canceled by burn.

####light
Only affects “dark” enemies. It temporarily removes their shroud, making them easier to hit, and causes
the attack with this flavor to deal more damage (again, only vs. dark enemies). 
`amt=1.2` means “Deal 120% damage against dark enemies.”

####area
Descriptive, does nothing by itself All area effect attacks, as well as splash regions of splash attacks, have this flavor.

####magic
Descriptive... Ice mage and healer attacks have this flavor, as do all of Azra’s and all enemys’ spells.

####physical
Descriptive... All attacks that aren’t magic have this flavor.

####melee	
Descriptive... This flavor triggers counter-attacks and "thorns" damage.

####ranged	
Descriptive... All arrows

####physical-ranged	
Descriptive... Rather than have the game check against things “physical” and “ranged” separately, 
we just created combination flavors for when we wanted to check for something specific. 
Worms in NG+ have a high rate of dodge versus this flavor, which basically means “arrows.”

####undodgeable
Makes the target skip their evasion check when resolving this attack. All parameters are ignored

####reduce_health
Used in Zelemir’s “decimate” spell. `amount=0.9` means “reduce health to 10%”
It reduces you to exactly that, and if you are below that amount, it will not do anything. Ie, this attack can’t kill you by itself.

####armor_pierce
Ignore a certain amount of armor when calculating damage. amount is multiplied against the attack’s 
damage to get the number of armor points ignored. So 100 DMG + armor pierce(amount=0.4), will ignore 40 points of armor.

####armor_ignore
Ignores armor altogether. All parameters ignored.

####armore_break
Removes a certain amount of armor permanently. amount of armor removed calculated the same way as for armor_pierce

####critical	
Damage is greater than normal `amount=2.2` means “Damage multiplier is 220%”

####knock_back	
Knocks an enemy back by a certain number of map squares. `amount=1.0` means “Knock back by 1 square length”. 1 square is 40x40 pixels

####auto_kill
same as devour, but without the “nom” Not used in game.

####devour
If target health is below a certain value, it dies immediately. `amount=0.1` means “if target is below 10% health, NOM!”

####strike_through
Attack can pierce (ie, keep going) and hit up to a certain number of targets amount=3 means “can hit up to 3 targets”

####de_invincible
Removes invincibility from affected target before applying damage.
Used in the “right hand” battle, when Zelemir attacks the super cultist - his 
lightning spell has “de-invincible” applied to it.

####psi_burn
Reduces the amount of PSI gained from killing affected enemy.
`amt=0.25` reduces PSI reward from target by (proportional_damage) x (25%)*

*psi_burn is complicated and needs further explaining. 
Basically, the higher the amount of psi_burn in an attack’s flavor, the less PSI an enemy hit with it will give when it dies.

Example:
    Azra has lightning with Damage(100)
    Azra strikes an Enemy(HP = 100, PSI_REWARD = 10) with lightning.

    If the lightning has psi_burn flavor (amount = 1.0):
    Enemy gives 0.0 PSI, all of it was burned away.
    Lightning dealt 100% of the enemy’s health.
    Flavor burned up 100% of its PSI
    
    If the lightning has psi_burn flavor (amount = 0.25):
    Enemy gives 7.5 PSI, 25% of it was burned away.
    Lightning dealt 100% of the enemy’s health.
    Flavor burned up 25% of its PSI
      
    If the enemy instead had 200 HP:
    After one strike, enemy will give 8.75 PSI when it dies.
    Lightning dealt 50% of the enemy’s health.
    Flavor burned up 12.5% of its PSI
    
    After two strikes, enemy will give 7.5 PSI when it dies (which is now)
    Lightning dealt another 50% of the enemy’s health
    Flavor burned up another 12.5% of its PSI

###Damage Flavors vs. Status Effects

Keep in mind, flavors are closely related to but not the same thing as status effects!
So, the “poison” flavor gives the corresponding “poison” status effect to anything that attack touches.
Likewise, the “inspire” flavor gives the “inspired” status effect to anything that attack touches.

So if you make a sword that has the “inspire” flavor or something, it will make all the enemies it hits become inspired,
making them deal more damage to you! Be careful about these things :) 
