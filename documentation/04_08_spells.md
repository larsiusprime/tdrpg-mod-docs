
##4.8 Mcguffin's Skills, Spells

Spells have probably undergone the biggest change from the original game to the DX engine.

Spells can be used by both defenders and enemies, and their master definitions are recorded in `spells.xml`, and then
referenced by specific defenders and enemies in `defender_skills.xml` and `enemy.xml`, respectively.

For now let's just treat all spells as hard-coded, and just look at how they are referenced with `defender_skills.xml`:

```xml
<skill name="lightning" type="attack" posture="offense">
	<reqs level="1" skill="none" skill_lvl="0"/>
	<info type="spell" spell="lightning"/>
	<flavor type="magic" amount="1.0" time="0.0" rate="1.0" />

	<flavor type="psi_burn" amount="1.0" time="0.0" rate="1.0" />
	<flavor type="undodgeable" amount="1.0" time="0.0" rate="1.0" />
	
	<stats level="1" x="20" y="0" z="0" cost="10" cooldown="0.25" x_add="0.5" x_stat="attack"/>
	<stats level="2" x="30" y="0" z="0" cost="10" cooldown="0.25" x_add="0.8" x_stat="attack"/>
	<stats level="3" x="50" y="0" z="0" cost="10" cooldown="0.25" x_add="1.1" x_stat="attack"/>
	<stats level="4" x="80" y="0" z="0" cost="10" cooldown="0.25" x_add="1.4" x_stat="attack"/>
	<stats level="5" x="120" y="0" z="0" cost="10" cooldown="0.25" x_add="1.7" x_stat="attack"/>
	<stats level="6" x="160" y="0" z="0" cost="10" cooldown="0.25" x_add="2.0" x_stat="attack"/>
	<stats level="7" x="200" y="0" z="0" cost="10" cooldown="0.25" x_add="2.3" x_stat="attack"/>
	<stats level="8" x="250" y="0" z="0" cost="10" cooldown="0.25" x_add="2.6" x_stat="attack"/>
	<stats level="9" x="300" y="0" z="0" cost="10" cooldown="0.25" x_add="2.9" x_stat="attack"/>
	<stats level="10" x="360" y="0" z="0" cost="10" cooldown="0.25" x_add="3.2" x_stat="attack"/>
	<stats level="11" x="420" y="0" z="0" cost="10" cooldown="0.25" x_add="3.5" x_stat="attack"/>
	<stats level="12" x="480" y="0" z="0" cost="10" cooldown="0.25" x_add="3.8" x_stat="attack"/>
	<stats level="13" x="550" y="0" z="0" cost="10" cooldown="0.25" x_add="4.1" x_stat="attack"/>
	<stats level="14" x="640" y="0" z="0" cost="10" cooldown="0.25" x_add="4.4" x_stat="attack"/>
	<stats level="15" x="730" y="0" z="0" cost="10" cooldown="0.25" x_add="4.7" x_stat="attack"/>
			
</skill>
```

Mcguffin Spells don't have anything in the info tag other than the type, which is "spell."

You can specify default flavors for the spell, though how that gets interpreted depends on the spell.

The stats table works like it does for techs/traits, but there are three very important values that only work for spells. These are:

```
    x - the value for the "x" variable in the spell.
    y - the value for the "y" variable in the spell
    z - the value for the "z" variable in the spell
    <var>_stat - lets you add a portion of one of the mcguffin's stats to the corresponding variable. 
                 So x_stat="attack" will add a portion of Azra's attack to the x variable.
    <var>_add  - this is the multiplier to use with <var>_stat. So x_stat="attack" and x_add="0.5" will 
                 add 50% of Azra's attack stat to base x value.
```

The _stat / _add thing is useful if you want a spell that can grow with the character's level, 
so lightning grows stronger as Azra grows stronger, not just based on raw skill points. 
Additionally, if you were to give Azra a weapon that buffs her attack stat, that would help in this case, too.

Now let's go look at spell definitions in `spells.xml`:

```xml
	<spell num="0" name="lightning" type="zap" cost="10" magnitude="0" sound="lightning" unique="true" txt="$SKILL_MCGUFFIN_A_LIGHTNING_DESC">
		<offset x="0" y="-0.5"/>
		<values x="25" y="0" z="0"/>
		<effect name="lightning" blend="add" times="0.25,0.4,0.1" alphas="1.0,1.0,0.0">
			<style thickness="3" color="white" displacement="200" detail="1" halo_colors="0x88AAEE,0x4444CC,0x334488"/>
		</effect>
		
		<!--damage one enemy or trigger one bomb, but not both!-->
		
		<action exclusive="true" verb="damage" damage="x" target_type="interactive" targets="1" radius="0.5" filter="bomb"/>
		<action exclusive="true" verb="damage" damage="x" target_type="enemy"       targets="1" radius="1.25"/>
		
	</spell>
```

###`<spell>` tag

```
num        which slot the spell appears in for the mcguffin interface in battle
name       the string identifier for this spell (I know I use "id" some places and "name" others -- really sorry about this...)
type       "zap" or "global" are the only two types right now. "zap" is basically a spell that cares about where you clicked to activate it,
           and "global" is one that doesn't.
cost       default psi casting cost. I think you can override this in the defender skill stat table
magnitude  0 or 1, affects which casting animation is used
sound      the id of the sound effect to play
unique     if true, removes any other active spell's visual effects when this is cast
txt        the description to show in the preview panel
```

###`<offset>` tag

This simply affects the positioning of the visual. Units are in battle squares.

###`<values>` tag

Lets you specify default x, y, and z variable values for this spell. Can be override in the defender skill stat table.

###`<effect>` tag

This is where you define the visual effect for the spell. Let's look at some examples:

```xml
<effect name="lightning" blend="add" times="0.25,0.4,0.1" alphas="1.0,1.0,0.0">
	<style thickness="3" color="white" displacement="200" detail="1" halo_colors="0x88AAEE,0x4444CC,0x334488"/>
</effect>
```

I'm pretty sure all "zap" style spells expect a "lightning" effect like this in order to work. `blend` is the 
photoshop-style blend mode to use, legal values should be "add", "multiply", "normal" ... and I'm not sure if any others actually work.

`times` and `alphas` are comma-separated numerical values that control the timing of the visual. The example here means:
```
@ time = 0.25 seconds, alpha = 1.0
@ time = 0.65 seconds, alpha = 1.0
@ time = 0.75 seconds, alpha = 0.0
```

Which means it will start off at 100% visibility until 0.65 secons have passed, then fade to nothing in 0.1 seconds.

The `style` tag controls the visuals of the lightning. Thickness and color are self-explanatory (should mention `color` can take 
a hexadecimal value or a limited number of simple standard color names), and `displacement` is how wild and crazy the lightning bolt will be (higher = more crazy).
With `detail`, a lower value means more detail and a higher value means less. The `halo_colors` are a comma-separated list of 
hexadecimal values that represent the glowing colors around the lightning.

Next we get to the actions, which are the heart of the spell:

```xml
		<action exclusive="true" verb="damage" damage="x" target_type="interactive" targets="1" radius="0.5" filter="bomb"/>
		<action exclusive="true" verb="damage" damage="x" target_type="enemy"       targets="1" radius="1.25"/>
```

Basically, this lightning spell can either trigger a bomb or strike a single enemy, but not both.

Contrast with "chain_lightning":

```xml
		<action exclusive="true" verb="damage" damage="x" target_type="interactive" targets="1"     radius="0.5" filter="bomb"/>
		<action exclusive="true" verb="damage" damage="x" attenuation="y" max_flavor_targets="stun:1" target_type="enemy" targets="level" radius="10.0"/>
```
Which can either trigger a bomb, or strike a number of enemies equal to the spell's level.

```
exclusive     if true, only one of these actions many occur. The first one in the list gets priority if both could happen.
verb          what the action does. Values are:
  "damage"        deal direct damage to target(s)
  "give_status"   give a status effect to target(s)
  "remove_status" remove a status effect from target(s)
  "heal"          heal target(s)
  "create"        create some battle object
  "splash"        launch a splash attack
  "boost"         boost a defender
  "heal_percent"  heal target(s) by a % rather than a constant value
damage        how much damage to deal (only used if the verb cares about damage)
hp            how much hp to heal (only used if the verb cares about healing)
target_type   "defender","enemy","creature"(a defender OR an enemy) or "interactive"
targets       "x","y","z","level","all" or a numerical value -- the number of things to target
radius        for a zap spell, the size of the targeting range, in battle squares. Centered on the clicked location.
              TODO: zap spell with a splash effect? 
filter        a string specifying the kind of thing you're looking for. The string id of an interactive, the class id of a defender, or the type id of an enemy
status        what status effect to use (for give_status or remove_status)
amount        the amount property of a status effect
time          the time property of a status effect
rate          the rate property of a status effect (default value is 1.0)
splash_time   the time the splash effect should last for
shape         the shape of a splash effect ("square" or "circle")
ally          for a boost verb, whether to target allies or not
not_mcguffin  if true, mcguffins are not targeted
not_ally      if true, allies are not targeted
scrutiny      value between 0.0 and 1.0 -- at 1.0 it always targets the closest target, at 0.0 it picks completely randomly from anything in range
```
