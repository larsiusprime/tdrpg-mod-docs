#Bonus Battle Tutorial

by James Cavin  
edited by Lars Doucet

##An awesome introduction

Hello all you bright and beautiful star children! Today we're going to talk about GLORIOUS BATTLES OUTSIDE OF SPACE AND TIME!

More specifically, we're going to be talking about HOW YOU CAN MAKE THEM!

That's right, Defender's Quest now has a… (drumroll, please) BONUS BATTLE EDITOR!

You see, as we create tools for Defender's Quest 2 development, we thought we'd retrofit them to work with DQ 1 and give them to all you adoring fans! Oh snap! (PLUS, as we expand tools for DQ 2 development, you'll get those expanded features too, so the tools we’re giving you are ONLY GOING TO GET BETTER WITH TIME! Double snap!)

So, hold onto your giblets and get ready to make your very own BONUS BATTLE MOD!

##Part 1: launching the thingy

First things first, you need to launch the LevelEditor!

![launch editor option](/images/launch_editor.png)

Okay, now you've got the editor running, you need to create a new project – a mod that will contain all of the bonus battles you're going to make! Click that new project button!

![editor](/images/editor.png)

You're going to be asked to give name for your mod – this is just a simple code identifier that the game will use as a handle for your project. I'm calling mine "legendsofawesome."

![selecting a project id](/images/project_id.png)
Next, it's going to ask you for a project title. The title is the thing that players are actually going to see. Mine is "Legends of Awesome."

![selecting a project title](/images/project_title.png)

CONGRATULATIONS! You've just made a *Defender's Quest* Mod! Of course, it doesn't have any battles or anything in it, but let's not let that detract from the glory of your accomplishment.

Have we sufficiently savored the moment? Good!

##Part 2: adding a battle to your project!

You'll notice that the path up at the top will say something like `blah blah blah/blah blah/blah/YOUR PROJECT NAME`

![editor with project loaded](/images/project_loaded.png)

That's right! We are INSIDE YOUR PROJECT!

Now to add a bonus battle!

…Click the button that says "new battle."

It's going to ask you for a battle ID – this is just the codename the game uses internally, so it doesn't need to be anything fancy. (Don't worry, you can give it a human-readable title befitting its awesomeness later.)

I'm naming mine "awesomeintro."

![selecting a battle id](/images/battle_id.png)

Wow! This thing looks kind of complicated!

![battle editor](/images/battle_editor.png)

Don't worry, we're going to break it down into nice bite-size pieces!

First of all, let's take a look at that upper right-hand menu. See that save button? Click it!

Congratulations, you have officially added a new bonus battle. Granted, it's a bonus battle with no place to put defenders and only a single enemy, but it's a bonus battle nonetheless!

Go ahead and take a moment to reflect on the awesomeness of your achievement. I'll wait.

Okay, ready to inject some kick ass into the equation?

##Part 3: put down something to defend!

See the big black square in the bottom left-hand corner? That's a preview of what your level looks like!

As you can see, it's not too much to look at right now. There's a big star marking where Azra will be, and a single enemy spawn point. So, how do we make with the mazes and chokepoints and as such?

Glad you asked! Take a look at the upper left-hand corner. See those 4 smaller black squares? This is where you're going to craft your murderous maze of magnificence by painting the different kinds of terrains that make up a Defender's Quest bonus battle.

The first pane allows you to place Azra's starting location, as well as the different spawn points for enemies. Let's go ahead and move Azra to a more interesting place than she is right now. See all the symbols underneath the pane? These are the different enemy spawn points (and Azra's start location) you can select and place. Click on the big 1 to select Azra's location. 

![selecting summoner location](/images/battle_editor_mcgloc.png)

Now you can click anywhere on this pane to put Azra there!

![placing summoner location](/images/battle_editor_mcgloc2.png)

I put her right in the middle of my map, but you are welcome to put her where ever you want – it's your canvas of carnage!

(On a side note, that big 1 you clicked on is a big 1 because, eventually, you will also be able to place second and third summoners, like Zelemir and Tletl-Meztli!)

You can also spice things up by adding more enemy spawn points! Just click on the symbol you want to place...

![selecting enemy location](/images/battle_editor_enemyloc.png)

...and then click anywhere on the locations pane to put the spawn point there! (You can right-click to erase a placed symbol, in case you made things too crazy.)

![placing enemy location](/images/battle_editor_enemyloc2.png)

##Part 4: Landscaping your playground of death

Okay, so we've got Azra and a bunch of enemy spawn points on the map, but there's still not much to look at – I mean, we don't even have any place to put defenders down!

Time to change all that! You see this pane to the right? This is a terrain pane – the place where you paint new kinds of terrain on to the battle! Right now, the selected terrain is LEGAL TERRAIN (grass). 

![legal terrain](/images/battle_editor_grass.png)

Defenders can be placed on legal terrain, and enemies can't walk on it. Why don't you slap down some legal terrain so the player can place defenders?

Pro tip: hold down the space button while clicking to fill open spaces! Go ahead and try it!

![fill terrain](/images/battle_editor_grass_fill.png)

Well shoot, we've got a problem: enemies can't walk on terrain, and we just filled the whole screen with it! This battle can't work – enemies will spawn and have no space to walk, leading to weird bugs.

Fortunately, we can right-click to erase terrain. Using this amazing ability, let's make some trails for our poor little revenant. Just erase terrain in a path from your different enemy spawn points to Azra's location.

![erase terrain](/images/battle_editor_grass_erase.png)

CONGRATULATIONS! You've created a fully functional bonus battle – the enemies can get to Azra, and there's legal terrain for the player to place defenders on!

##Part 5: what about those other panes?

So you're probably wondering what those other 2 panes are for. Well, as you can imagine there's far more than a single kind of terrain in Defender's Quest. That's right, these other panes are where you can lovingly paint even more luscious real estate on your garden of gore!

By default, they are ILLEGAL TERRAIN and WATER.

The player can't place defenders on illegal terrain, AND enemies can't walk on it. You can put down illegal terrain to make the level harder – decreasing the places where player can put their defenders.

Water is kind of similar – the player can't put defenders on water, and most enemies can't walk on it. HOWEVER, special water enemies can walk through water just like it's a regular path!

Go ahead and play around with placing some illegal terrain and water. It's your bonus battle, go nuts! (Just remember that each enemy spawn point still needs a path to Azra.)

![multiple terrain types](/images/battle_editor_multiterrain.png)

As you can see in the preview, all of the panes layer to create the final level. You can even click the little left and right arrows over a pane to change the order in which they're layered on top of one another. When you have multiple terrains on top of each other, it's the topmost one that takes effect. (So an illegal tile on top of a legal tile means the tile counts as illegal for gameplay purposes, while a legal tile on top of an illegal tile makes it count as legal.) You can always tell what kind of terrain the final tile will count as by looking at the preview – whatever shows up on top is what it is.

So what's that little "…" button over each pane? 

![change terrain button](/images/battle_editor_ellipses.png)

Clicking this button opens up a list of all of the terrains in the game (which we've handily presorted for you because that's how much we care). 

![battle editor blue sand](/images/battle_editor_blue_sand.png)

You didn't think we're going to stick you with the default grass, rocks, and water, did you? It's your bonus battle, pick whatever kinds of terrain you want! (You can even click the "…" button over the start locations pane to set what the empty background tile should be.)

The second-to-last category of terrain, "art," is special art pieces we used in some of our story battles. They don't have any terrain effects, but you can use them to add some flavor to your battles.

If you don't like a pane, you can erase the whole thing with the X button over it. 

![battle editor delete layer](/images/battle_editor_x.png)

You can even create more panes with the gigantic + to the right!

![battle editor add layer](/images/battle_editor_plus.png)

You can use many different kinds of legal, illegal, and water terrains in a single battle. Try using different layers to create strange artistic effects!

![battle editor hanging gardens](/images/battle_editor_hanging_gardens.png)

##A hint about water

In my level, I created some shortcuts on my enemy paths and then filled them with water. Now when special water enemies show up, they can take these unexpected shortcuts and catch the player by surprise!

![battle editor water](/images/battle_editor_water.png)

##Part 6: unleashing the hordes!

See that second bar on the right? That's a wave bar – the place where you set how many enemies come charging at Azra from where!

![battle editor waves](/images/battle_editor_waves.png)

At the far left of the bar, there's all of the symbols for the enemy spawn points – click on one of these symbols to tell the enemies in this wave to emerge from this spawn point.

![battle editor select wave spawn points](/images/battle_editor_waves_spawns.png)

A single wave of enemies can come from multiple spawn points. I'm clicking both of the spawn points I have on the map, so my wave is going to spawn from both locations! (You can click on a spawn point symbol again to unselect that spawn point).

Next, you'll see a big button that says "Normal." This is where you set what kind of enemy this wave is made up of. Go ahead and click on it. 

![battle editor select enemy type](/images/battle_editor_enemies.png)

BAM! That's a list of every enemy in the game, son! HORDES OF EVIL ARE AT YOUR DISPOSAL.

I set my wave of enemies to the Attacker type (the red revenant that claw defenders as they walk past), because I like it when my defenders get punched back, but that's just me. You have dozens of enemies to pick from – do whatever you want! You can even select sheep!

Next, you'll see a text field labeled "count." This is how many enemies of the type selected are in this wave. Right now, it's just 1, which isn't particularly fear-inspiring. Let's jazz things up a little bit. How about 30 enemies?!

![battle editor set number of enemies](/images/battle_editor_waves_count.png)

The "wait" field lets you set how much time the player has between this wave and the next one. I'm leaving mine at 1 second. 

![battle editor set wait](/images/battle_editor_waves_wait.png)

For the delay before the first wave appears, change the "first wait" amount in the section just above this.

![battle editor set first wait](/images/battle_editor_first_wait.png)

The "level" field lets you set how tough the enemies in this wave are. Let's make this a bit of a challenge… I'm setting my enemies at level 15!

![battle editor set level](/images/battle_editor_wave_level.png)

Rate is how fast these enemies are spawned, measured in enemies per second. I'm setting mine to 2, so one enemy will be appearing every half second!

![battle editor set rate](/images/battle_editor_wave_rate.png)

OKAY, we've got a single wave of  enemies coming at the player! That's definitely more challenging than 1 enemy, but still not as awesome as I would like. IT'S TIME TO ADD ANOTHER WAVE.

Just click the big + underneath the wave bar. 

![battle editor add wave](/images/battle_editor_add_wave.png)

Bam! There's a whole new wave!

![battle editor new wave](/images/battle_editor_new_wave.png)

I'm gonna mix things up with a wave of 20 fast worms coming in after a pause of 10 seconds. You do whatever you want! It's your bonus battle!

![battle editor change wave settings](/images/battle_editor_wave2.png)

Finally, I'm going to do a surprise wave of water enemies! (Any name with _W after it is a water enemy. I picked normal_w, but there's plenty of other options.) These surprise water enemies will take advantage of those shortcuts I made earlier!

![battle editor third wave](/images/battle_editor_wave3.png)

In theme with this surprise jackass move, I'm going to add one final wave that's nothing but a middle finger. (Yes, that's an enemy type!)

![battle editor finger wave](/images/battle_editor_wave4.png)

##Part 7: sweet sweet loots!

Okay, so we've got a bunch of enemies for the player to mash now. The only thing left is some sweet, sweet loot waiting at the end!

This takes us to the first bar on the right side of the screen – this is where we control various battle settings.

![battle editor settings](/images/battle_editor_settings.png)

"First wait" is how much time the player has at the start of the battle before enemy waves appear. I'm going to give my players a solid 10 seconds.

![battle editor set first wait](/images/battle_editor_first_wait2.png)

Next, we can set how many gold and blue stars are required for this battle to become available in the bonus battle menu. 

![battle editor set unlock stars](/images/battle_editor_star_button.png)

(The requirement can be set independently for new game plus, so you can make your battle harder or easier to unlock on a second play through of the game.) The battle I made isn't super scary, so I'm going to set it to 20 blue stars. Players will be able to play my battle once they've earned 20 blue stars through story battles! For new game plus, I'm changing the requirement to gold stars – these are the big leagues kiddo, step up your game!

![battle editor change unlock stars](/images/battle_editor_stars.png)

Next, you have the "endless" checkbox. 

![battle editor endless](/images/battle_editor_endless.png)

Clicking this will turn your battle into an endless battle – the waves you've designed will repeat infinitely. Each time they repeat, the levels of the monsters will increase by the amount you enter in the "Endless level up" field. For the moment, I just want to make a normal battle – I'll come back and show you guys the ins and outs of endless battles later.

Finally, we get to the good stuff: REWARDS!

You'll notice there's 2 reward buttons. For normal (non-endless) battles, the first button is the reward players get for winning the battle with Azra taking some hits (what would earn you a blue star in a story battle). The second button is for a perfect score – battle beaten without a single enemy getting to Azra (a gold star in story battles).

![battle editor reward buttons](/images/battle_editor_reward_buttons.png)

Clicking one of these brings up a menu to adjust the reward settings.

![battle editor reward settings](/images/battle_editor_reward_settings.png)

You'll also notice that each button lets you set rewards independently for the regular play through and new game plus, so you can make the battle have much higher payouts in new game plus!

The "type" button lets you pick what kind of reward the player is going to get: experience, "gold" (the in-game currency is actually "scrap", but in the game's code it's just called "gold"), an item, or nothing.

We'll get into items later – for the moment, I'm making my rewards hard, cold cash! A normal pass gets you 500 gold, and a perfect pass gets you 1500! GETTING PAID.

![battle editor reward settings](/images/battle_editor_reward_settings2.png)

##Part 8: put a bow on it

All right, you've got a battle with spawn points, trails, shortcuts, hordes of enemies, and tons of sweet loot sitting at the end! Time to put a bow on it and present your glorious masterpiece to the world!

First of all, you need a title befitting the resplendent awesomeness of your creation. TO THE TITLE BUTTON!

![battle editor title button](/images/battle_editor_title_button.png)

**NOTE TO SELF: Fix crash bug that happens here**

Go to the upper right-hand of the screen, and click the big button labeled "title." This gives you a place to enter a title for the battle – the human readable name that players will see when they select your shining gem of maze-based violence. This will pop up a weird little screen that looks like this.

![battle editor change title](/images/battle_editor_title.png)

Click the flag at the top to select the language you are entering text for. (Sorry to all of you Australians, New Zealanders, and various British Islanders – we only speak American here!)

You can enter the text directly by just typing on your keyboard, but if you have any trouble with certain language/keyboard combinations (such as Chinese, Japanese, Korean, etc), we have a safety fallback - you can open an external editor, enter the text correctly there, copy it to your clipboard, and then click "PASTE from clipboard" in the editor to get the text directly, with no input shenanigans getting in the way.

My title is "The Awesomeness Begins…"

![battle editor enter english title](/images/battle_editor_title2.png)

In Spanish that'd probably be something like "Comienza la Awesomeness..."
(I skipped consulting with our Spanish translator on that one.)

![battle editor enter spanish title](/images/battle_editor_title3.png)

Let me give an example of how you'd enter a Chinese title. Rather than accidentally writing something 
that translates to "Fart sauce" or whatever, I'll just cheap out and use the title of the famous Chinese
Epic, "Journey to the West." We can find the Chinese characters for that [on Wikipedia](https://en.wikipedia.org/wiki/Journey_to_the_West):

![journey to the west](/images/journeytothewest.png)

I select that text, right click, copy. Now it's in my system clipboard. I click the chinese flag with
the red background (for Simplified Chinese) and then click the "PASTE from clipboard" button and now
I've got the Chinese text in. You can do the same for any language that's tricky to enter text directly for.

![battle editor enter chinese title](/images/battle_editor_title4.png)

Next, give your battle a little bit of descriptive flavor text! Click the BLURB BUTTON!

This works exactly like the title field – just paste the text you want in there, click accept and BAM! you've got a little blurb full of descriptive flavor text! Mine says "…This time it's personal."

![battle editor blurb](/images/battle_editor_blurb.png)

And that's it!

Wait, one last thing... don't forget to save your changes.

![battle editor save](/images/battle_editor_save.png)

YOUR BONUS BATTLE IS NOW READY FOR THE WORLD!!!

##Part 9… Play that sexy thang!

Okay, let's PLAY your awesome bonus battle. This is easy, just launch Defender's Quest and go to the save slot screen.

Click on the "mods" button in the lower right (it's a wrench).

![Defender's Quest save slot screen w/ mods button](/images/dqmodbutton.png)

Select "My Mods", then "Okay."

![Mods menu](/images/dqmods.png)

The mod browser appears, and here's your mod! The mod I created adds exactly one bonus battle to the game. To play a single mod, just click on it and then hit "Play."

![Play mod](/images/legendsofawesome.png)

This will restart Defender's Quest with the mod loaded. You can tell if a mod is loaded by looking at the bottom right of the title screen.

![Defender's Quest with mod loaded](/images/modloaded.png)

We hit start and... hey! Where'd our save files go?

![Defender's Quest with no saves](/images/dqemptysaves.png)

Well, the thing is that mods technically let you change almost *anything* about the game, which means that save files from the regular game aren't guaranteed to work with it, so we make sure that each mod has its own save directory that's totally independent from the regular game, just to be sure. The stuff we made in this tutorial should be totally safe, though, so let's go ahead and import a save file from the regular game.

![Import save file](/images/dqsaveimport.png)

I'm going to select this save file I've prepared.

![Select save file](/images/dqimportsavefile.png)

Starting that save, and proceeding to the bonus battle menu, I see this:

![New bonus battle](/images/newbonusbattle.png)

Bonus battles are sorted by the unlock requirement from least to greatest, with blue stars counting as 0.5 gold stars, so our new bonus battle shows up on top.

Selecting it shows the preview...

![Bonus battle preview](/images/newbonusbattlepreview.png)

And there it is! Our bonus battle is in the game!

![Play bonus battle](/images/playbonusbattle.png)
