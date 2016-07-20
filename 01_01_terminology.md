##1.1. Terminology for n00bs

Feel free to skip this section and refer back to it later as necessary.

You don’t need any programming experience to make a Defender’s Quest mod, but throughout this documentation I will be using some light programming jargon, as well as some terminology specific to Defender’s Quest. Here’s a quick rundown:

###Defender’s Quest Jargon:

**TD-RPG:**
This means “Tower Defense Role Playing Game” and was the original code-name for the project.

**Labels vs. Variables:**
A label is the piece of text that we display to the player in game and is consistent with the game’s theme and story. Often we’ll have an internal representation of that thing in game data that goes by some other name, sometimes similar, sometimes completely different, and often has no relation to the game’s theme, it’s just a mechanical word for our own use. This internal representation is called a “variable.” The following entry is a good example.

**Mcguffin:**
Although Azra’s character class is displayed as “Librarian” in game, her character class is referred to throughout the code and game data as “mcguffin.” This is because she is the “Tower Defense McGuffin”, ie the thing you have to arbitrarily defend.

**Unazra:**
The mysterious sorceress, Tletl-Metzli, was originally named “unazra” while we were coming up with a name for her, and this is what she’s referred to in game data. Her character class is “antimcguffin.”

**Gold/scrap:**
Scrap is the in-game label for money, but in data the variable is simply “gold” (usually).

**Defender vs. Character:**
The members of your party are your characters, and the units you place in battle are defenders. This distinction is pretty subtle, but I throw it in as a heads-up for when you see me use one or the other term.

A character is an object that holds a party member’s data, basically, and a defender is the in-battle representation for that character. Azra is also a “defender” in this sense.

**Creature:**
In battle, the word “creature” means either a defender or an enemy. So, when I say something like “creatures can take damage” I mean, “defenders or enemies can take damage.”
Casual/Normal/Advanced/Extreme:
The battle challenge labels are “casual”, “normal”, “advanced,” and “extreme,” but internally the variables are “casual”, “easy”, “medium,” and “hard.”

**Alternate Mcguffin, Allies, and Minions:**
In the final battle, Zelemir shows up as a support character and alternate target for the enemies and is thus an “alternate mcguffin.” When Unazra shows up, she is sometimes an alternate mcguffin (the final sidequest) but usually simply a substitute mcguffin for Azra.

- Every battle always has at least one **mcguffin**
  - In battles with more than one **mcguffin**, only one is the **primary mcguffin** (in DQI this is usually Azra).
  - In battles with more than one **mcguffin**, all non-primary mcguffins are **alternate mcguffins**.
  - Mcguffins are immune to global spells such as "dragon fire" and will not be targeted by conventional enemy attacks
  - Mcguffins can only be harmed by enemies reaching their location
  - In DQI, a mcguffin is indicated by appearing at the beginning of the level, standing on a blue crater
- Any computer-controlled defender is called an **ally**. An ally may or may not be a mcguffin:
  - Tletl-Meztli in the final sidequest is technically a mcguffin, but no enemies actually target her location
  - Zelemir at the end of "Eztli-Tenoch's right hand" is NOT a mcguffin, and wholly controlled by a triggered script
  - Zelemir in the final battle is both technically and functionally a mcguffin, enemies target him separately from Azra
- Some defenders can summon **minions** that are largely computer controlled and simpler than full defenders.
  - This feature is NOT used in DQI, only in DQII:
    - The Weaselmancer's weasels
    - The Beast Master's beasts

###Programming Jargon:

**String:**
Some text, i.e, a ‘string” of letters, numbers, or other characters between quote marks. Not the stuff you tie up packages with.

Examples:
```
  "this_is_a_string"
  "this is also a string"
  "aNdIAmaStringT00!!!11110mgroflcopter"
```

**Boolean:**
A value that is either true or false. Sometimes called a "bool" for short.

**Byte:**
Eight “bits” of memory, where a bit is a number that can store only a zero or a one. A byte can store any number between 0 and 255, or 256 values in total.

**Hexadecimal:**
Regular numbers are base 10, so “10” means “ONE ten + ZERO ones.”
Binary numbers are base 2, so “10” means “ONE two + ZERO ones.”

Hexadecimal numbers are base 16, so “10” means “ONE sixteen + ZERO ones.” Since you can go higher than ten for a single digit in Hexadecimal you need extra characters to display those values. So, you use letters of the alphabet. “A” means ten, “B” means eleven, etc, up to “F” which means fifteen. So, “1B” in Hexadecimal means “ONE sixteen + ELEVEN ones,” or 27 in decimal.

The only reason I go into this much detail is because color values are often expressed in Hexadecimal. So, on a computer, a single pixel on the screen is defined by three numbers, each specifying the amount of red, green, and blue light. These three values are the red, green, and blue color “channels.”

Take the color magenta. On a computer, magenta is made by mixing the maximum amount of red and blue light, with no green light. So, one byte (0-255) is used for each color “channel.”

Magenta = Red(255) + Green(0) + Blue(255).
In Hexadecimal, 255 is written as `FF`.
(FIFTEEEN sixteens + FIFTEEN ones) = (15x16 + 15) = (240+15) = 255.

So Magenta = Red(FF) + Green(00) + Blue(FF).

Usually you stick those three bytes together: `FF00FF`, and to let the computer know that’s a hexadecimal number rather than a regular string, you put `0x` in front. So magenta is commonly expressed as `0xFF00FF` in Hexadecimal.

**24-bit vs.32-bit color**
As you might have guessed, the 3 bytes of a pixel equals 24 bits. So, that’s where the word “24-bit color” comes from - 24-bit pixels. So what does “32-bit color” mean? Well, sometimes you want pixels that are partially transparent. To do this, you add one more “channel,” the “alpha channel,” where alpha means transparency. In a 32-bit pixel value, the first byte is the transparency value, where 0 means “fully transparent” and 255 means “fully visible.”

So `0xFFFF00FF` would be completely visible magenta, and `0x88FF00FF` would be half-transparent magenta, and `0x00FF00FF` would be completely invisible magenta, the same as not drawing anything at all.

Throughout the mod data, if you see me using only six letters for a color, (not counting the “0x” prefix) then I’m using 24-bit color and you don’t have to worry about transparency. This is the RGB format - the first byte is red, then green, then blue. If I’m using 8 letters for a color, it’s in a place where I need transparency, so I’m using 32-bit color. This is the ARGB format - the first byte is alpha (transparency), then red, then green, then blue. 
