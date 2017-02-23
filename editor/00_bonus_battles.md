#Bonus Battle Tutorial

by James Cavin

##An awesome introduction

Hello all you bright and beautiful star children! Today we're going to talk about GLORIOUS BATTLES OUTSIDE OF SPACE AND TIME!

More specifically, we're going to be talking about HOW YOU CAN MAKE THEM!

That's right, Defender's Quest now has a… (drumroll, please) BONUS BATTLE EDITOR!

You see, as we create tools for Defender's Quest 2 development, we thought we'd retrofit them to work with DQ 1 and give them to all you adoring fans! Oh snap! (PLUS, as we expand tools for DQ 2 development, you'll get those expanded features too, so the tools we’re giving you are ONLY GOING TO GET BETTER WITH TIME! Double snap!)

So, hold onto your giblets and get ready to make your very own BONUS BATTLE MOD!

##Part 1: launching the thingy

First things first, you need to launch the LevelEditor!

![launch editor option](larsiusprime.github.com/tdrpg-mod-docs/editor/images/launch_editor.png)

Okay, now you've got the editor running, you need to create a new project – a mod that will contain all of the bonus battles you're going to make! Click that new project button!

You're going to be asked to give name for your mod – this is just a simple code identifier that the game will use as a handle for your project. I'm calling mine "legendsofawesome."

Next, it's going to ask you for a project title. The title is the thing that players are actually going to see. Mine is "Legends of Awesome."

CONGRATULATIONS! You've just made a Defender's Mod! Of course, it doesn't have any battles or anything in it, but let's not let that detract from the glory of your accomplishment.

Have we sufficiently savored the moment? Good!

##Part 2: adding a battle to your project!

You'll notice that the path up at the top will say something like "blah blah blah/blah blah/blah/YOUR PROJECT NAME"

That's right! We are INSIDE YOUR PROJECT!

Now to add a bonus battle!

…Click the button that says "new battle."

It's going to ask you for a battle ID – this is just the codename the game uses internally, so it doesn't need to be anything fancy. (Don't worry, you can give it a human-readable title befitting its awesomeness later.)

I'm naming mine "awesomeintro."

Wow! This thing looks kind of complicated!

Don't worry, we're going to break it down into nice bite-size pieces!

First of all, let's take a look at that upper right-hand menu. See that save button? Click it!

Congratulations, you have officially added a new bonus battle. Granted, it's a bonus battle with no place to put defenders and only a single enemy, but it's a bonus battle nonetheless!

Go ahead and take a moment to reflect on the awesomeness of your achievement. I'll wait.

Okay, ready to inject some kick ass into the equation?

##Part 3: put down something to defend!

See the big black square in the bottom left-hand corner? That's a preview of what your level looks like!

As you can see, it's not too much to look at right now. There's a big star marking where Azra will be, and a single enemy spawn point. So, how do we make with the mazes and chokepoints and as such?

Glad you asked! Take a look at the upper left-hand corner. See those 4 smaller black squares? This is where you're going to craft your murderous maze of magnificence by painting the different kinds of terrains that make up a Defender's Quest bonus battle.

The first pane allows you to place Azra's starting location, as well as the different spawn points for enemies. Let's go ahead and move Azra to a more interesting place than she is right now. See all the symbols underneath the pane? These are the different enemy spawn points (and Azra's start location) you can select and place. Click on the big 1 to select Azra's location. Now you can click anywhere on this pane to put Azra there!

I put her right in the middle of my map, but you are welcome to put her where ever you want – it's your canvas of carnage!

(On a side note, that big 1 you clicked on is a big 1 because, eventually, you will also be able to place second and third summoners, like Zelemir and Tletl Meztli!)

You can also spice things up by adding more enemy spawn points! Just click on the symbol you want to place, and then click anywhere on the locations pane to put the spawn point there! (You can right-click to erase a placed symbol, in case you made things too crazy.)

##Part 4: Landscaping your playground of death

Okay, so we've got Azra and a bunch of enemy spawn points on the map, but there's still not much to look at – I mean, we don't even have any place to put defenders down!

Time to change all that! You see this pane to the right? This is a terrain pane – the place where you paint new kinds of terrain on to the battle! Right now, the selected terrain is LEGAL TERRAIN (grass). Defenders can be placed on legal terrain, and enemies can't walk on it. Why don't you slap down some legal terrain so the player can place defenders?

Pro tip: hold down the space button while clicking to fill open spaces! Go ahead and try it!

Well shoot, we've got a problem: enemies can't walk on terrain, and we just filled the whole screen with it! This battle can't work – enemies spawn and have no space to walk.

Fortunately, we can right-click to erase terrain. Using this amazing ability, let's make some trails for our poor little revenant. Just erase terrain in a path from your different enemy spawn points to Azra's location.

CONGRATULATIONS! You've created a fully functional bonus battle – the enemies can get to Azra, and there's legal terrain for the player to place defenders on!

##Part 5: what about those other panes?

So you're probably wondering what those other 2 panes are for. Well, as you can imagine there's far more than a single kind of terrain in Defender's Quest. That's right, these other panes are where you can lovingly paint even more luscious real estate on your garden of gore!

By default, they are ILLEGAL TERRAIN and WATER.

The player can't place defenders on illegal terrain, AND enemies can't walk on it. You can put down illegal terrain to make the level harder – decreasing the places where player can put their defenders.

Water is kind of similar – the player can't put defenders on water, and most enemies can't walk on it. HOWEVER, special water enemies can walk through water just like it's a regular path!

Go ahead and play around with placing some illegal terrain and water. It's your bonus battle, go nuts! (Just remember that each enemy spawn point still needs a path to Azra.)

As you can see in the preview, all of the panes layer to create the final level. You can even click the little left and right arrows over a pane to change the order in which they're layered on top of one another. When you have multiple terrains on top of each other, it's the topmost one that takes effect. (So an invalid tile on top of a valid tile means the terrain is invalid, while a valid tile on top of an invalid tile makes it valid.) You can always tell what kind of terrain the player will get by just looking at the preview – whatever you can see is what there is.

So what's that little "…" button over each pane? Clicking this button opens up a list of all of the terrains in the game (which we've handily presorted for you because that's how much we care). You didn't think we're going to stick you with the default grass, rocks, and water, did you? It's your bonus battle, pick whatever kinds of terrain you want! (You can even click the "…" button over the start locations pane to set what the empty background looks like.)

The last category of terrain, "art," is special art pieces we used in some of our story battles. They don't have any terrain effects, but you can use them to add some flavor to your battles.

If you don't like a pane, you can erase the whole thing with the X button over it. You can even create more panes with the gigantic + to the right!

You can use many different kinds of legal, illegal, and water terrains in a single battle. Try using different layers to create strange artistic effects!


##A hint about water

In my level, I created some shortcuts on my enemy paths and then filled them with water. Now when special water enemies show up, they can take these unexpected shortcuts and catch the player by surprise!

##Part 6: unleashing the hordes!

See that second bar on the right? That's a wave bar – the place where you set how many enemies come charging at Azra from where!

At the far left of the bar, there's all of the symbols for the enemy spawn points – click on one of these symbols to set the enemies in this wave to come from this spawn point. A single wave of enemies can come from multiple spawn points. I'm clicking both of the spawn points I have on the map, so my wave is going to spawn from both locations! (You can click on a spawn point symbol again to unselect that spawn point).

Next, you'll see a big button that says "Normal." This is where you set what kind of enemy this wave is made up of. Go ahead and click on it. BAM! That's a list of every enemy in the game, son! HORDES OF EVIL ARE AT YOUR DISPOSAL.

I set my wave of enemies to the Attacker type (the red revenant that claw defenders as they walk past), because I like it when my defenders get punched back, but that's just me. You have dozens of enemies to pick from – do whatever you want! You can even select sheep!

Next, you'll see a text field labeled "count." This is how many enemies of the type selected are in this wave. Right now, it's just 1, which isn't particularly fear-inspiring. Let's jazz things up a little bit. How about 30 enemies?!

The "wait" field lets you set how much of a pause the player has before this wave comes. I'm leaving mine 1 second.

The "level" field lets you set how high leveled the enemies in this wave are. Let's make this a bit of a challenge… I'm setting my enemies at level 15!

Rate is how fast these enemies are spawned, measured in enemies per second. I'm setting mine to 2, so an enemy will be appearing every half second!

OKAY, we've got a single wave of  enemies coming at the player! That's definitely more challenging than 1 enemy, but still not as awesome as I would like. IT'S TIME TO ADD ANOTHER WAVE.

Just click the big + underneath the wave bar. Bam! There's a whole new wave!

I'm gonna mix things up with a wave of 20 fast worms coming in after a pause of 10 seconds. You do whatever you want! It's your bonus battle!

Finally, I'm going to do a surprise wave of water enemies! (Any name with _W after it is a water enemy. I picked normal_w, but there's plenty of other options.) These surprise water enemies will take advantage of those shortcuts I made earlier!

In theme with this surprise jackass move, I'm going to add one final wave that's nothing but a middle finger. (Yes, that's an enemy type!)

##Part 7: sweet sweet loots!

Okay, so we've got a bunch of enemies for the player to mash now. The only thing left is some sweet, sweet loot waiting at the end!

This takes us to the first bar on the right side of the screen – this is where we control various battle settings.

"First wait" is how much time the player has at the start of the battle before enemy waves appear. I'm going to give my players a solid 10 seconds.

Next, we can set how many gold and blue stars are required for this battle to become available in the bonus battle menu. (The requirement can be set independently for new game plus, so you can make your battle harder or easier to unlock on a second play through of the game.) The battle I made isn't super scary, so I'm going to set it to 20 blue stars. Players will be able to play my battle once they've earned 20 blue stars through story battles! For new game plus, I'm changing the requirement to gold stars – these are the big leagues kiddo, step up your game!

Next, you have the "endless" checkbox. Clicking this will turn your battle into an endless battle – the waves you've designed will repeat infinitely. Each time they repeat, the levels of the monsters will increase by the amount you enter in the "Endless level up" field. For the moment, I just want to make a normal battle – I'll come back and show you guys the ins and outs of endless battles later.

Finally, we get to the good stuff: REWARDS!

You'll notice there's 2 reward buttons. For normal battles, the first button is the reward players get for winning the battle with Azra taking some hits (what would earn you a blue star in a story battle). The second button is for a perfect score – battle beaten without a single enemy getting to Azra.

You'll also notice that each button lets you set rewards independently for the regular play through and new game plus, so you can make the battle have much higher payouts in new game plus!

The "type" button lets you pick what kind of reward the player is going to get: experience, "gold" (the in game currency is actually scrap, but in the game's code gets called gold), an item, or nothing.

We'll get into items later – for the moment, I'm making my rewards hard, cold cash! A normal pass gets you 500 gold, and a perfect pass gets you 1500! GETTING PAID.

##Part 8: put a bow on it

All right, you've got a battle with spawn points, trails, shortcuts, hordes of enemies, and tons of sweet loot sitting at the end! Time to put a bow on it and present your glorious masterpiece to the world!

First of all, you need a title befitting the resplendent awesomeness of your creation. TO THE TITLE BUTTON!

Go to the upper right-hand of the screen, and click the big button labeled "title." This gives you a place to enter a title for the battle – the human readable name that players will see when they select your shining gem of maze-based violence. This will pop up a weird little screen that looks like this.

Click the flag at the top to select the language you are entering. (Sorry to all of you Australians, New Zealanders, and various British Islanders – we only speak American here!)

Next, PASTE the text you want into the text field. (For a wide variety of technical reasons we don't allow you to type directly into the field – I apologize, but you'll just have to type out your title in one of the bajillion text editors available and then copy and paste it into the title field.)

My title is "The Awesomeness Begins…"

Next, give your battle a little bit of descriptive flavor text! Click the BLURB BUTTON!

This works exactly like the title field – just paste the text you want in there, click accept and BAM! you've got a little blurb full of descriptive flavor text! Mine says "…This time it's personal."

And that's it!

YOUR BONUS BATTLE IS READY FOR THE WORLD!!!

##Part 9… Play that sexy thang!
