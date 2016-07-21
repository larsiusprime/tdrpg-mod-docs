
##4.7 Passive Skills, "Traits"

Traits are much simpler than techniques.

As far as I can tell, there are only two valid "type" values for traits, "flavor" and "stat_boost".

###Flavor augments
Most passive traits just add new flavors to your attacks.
This sounds pretty simple, but can do all kinds of interesting new things for your characters.

Specifying this is really simple:
```xml
<info type="flavor" flav="poison" attack="all" />
```

Now this stat will give "poison" to all attacks, and you specify the amount/time/rate values in the stats table like so:

```xml
<stats level="1" amount="0.07" time="10" rate="0.02" />
<stats level="2" amount="0.08" time="11" rate="0.025" />
<stats level="3" amount="0.09" time="12" rate="0.03" />
<stats level="4" amount="0.10" time="13" rate="0.035" />
```

You can also specify the id of an attack instead of "all", and the flavor will only be added to that specific attack.

###Stat boost
This one's even simpler.

You identify the stat to boost:
```xml
<info type="stat_boost" stat="range" />
```

And specify how much in the stats table:
```xml
<stats level="1" amount="0.20" />
<stats level="2" amount="0.30" />
<stats level="3" amount="0.40" />
<stats level="4" amount="0.50" />
```

**NOTE:** *the amount is the TOTAL BONUS at that skill level, it doesn't cumulatively add all the previous ones. *
