##4.4 Skills

Skills are at the very heart of defender's quest.

There's two basic kinds: passive skills, or TRAITS, and active skills/attacks, or TECHNIQUES.

Each character will have exactly 5 TECHNIQUES, except for Azra, who has 6 spells that take the place of techniques. Each character also has a varying number of traits, except for Azra, who has none.

Each `<defender>` tag will reference the class id, and then have a list of `<skill>` tags.

`<skill>` tag

```
  name    - the reference id for the skill. Used all over the place.
  type    - legal values are "attack" for a technique or "passive" for a trait
  posture - legal values are "offense" and "defense" and is mostly cosmetic (red vs. blue)
```

The sub tags are:

```
  reqs        - requirements to unlock
  flavor      - list of flavors associated with the skill
  graphic     - associated graphics/animations
  graphic_pos - offset values (if necessary)
  info        - very important, specifies almost everything about the skill
  stats       - provides a table of stat values for each skill point invested
```

`<reqs>`
Requirements. "level" specifies which level the character must be at to unlock this skill, "skill" specifies what skill is a prerequisite for this (put "none" if none), and "skill_lvl" specifies how many points you need in the prerequisite to unlock it.

`<flavor>`
Each flavor tag specifies a "flavor" that can be applied to the skill. Flavors modify attacks in various ways. Most skills will have boring flavors like "physical" and "melee" that are (mostly) descriptive. These generally don't do anything special other than identify the source of damage, in case a creature is strong/weak against it, etc. Some attacks, however, have flavors like "chill" and "burn" that do cool stuff.

All flavors specified here are ALWAYS ON for this attack. They may be modified and/or replaced by traits, or by the stats table, but otherwise whatever is specified here will always show up on the attack.

See the "Damage Flavors" section below for more about flavors.

The remaining tags will also be discussed in the following sections. 
