#Translation guide

This document explains the basic procedure for how to get your translation files into the game itself so you can see the effect on the game immediately, which aids with context.

##Step 1: Create a localization-only mod

In the game, go to the save slot screen, and click on the Mods button (the wrench)

![](/images/translate/modsbutton.png)

Select "Create new", then click Okay.

![](/images/translate/createnew.png)

Make sure only "Core data files" is selected, and click Select.

![](/images/translate/coredata.png)

Enter a name for the mod and click Accept.

**NOTE:** *This will create a mod that contains a copy of all the game's basic data files, but none of its art, music, or battle data.*

![](/images/translate/modname.png)

Wait for the export to complete, then click "Explore."

![](/images/translate/exportcomplete.png)

This will bring up the folder with all your mods. Open the folder with the same name as your mod.

![](/images/translate/modsfolder.png)

Open the folder, then select the "monologue", "tables", "tiled", and "xml" folders, and delete them. You won't need them.

**NOTE:** *Since we only want to create a mod that adds a new language, we do not need these data files. If they are not included in the mod, the game will revert to the default versions of these files.*

![](/images/translate/deletefolders.png)

Next, open the "locales" folder

![](/images/translate/selectlocale.png)

Select all the locales that you will not be changing and delete them.

![](/images/translate/deletelocales.png)

Open the folder of the locale you wish to change:

![](/images/translate/selectmylocale.png)

To update the translation, just copy and paste new files into this folder. Just make sure they're correctly formatted.

![](/images/translate/dropfiles.png)

##Step 2: Load your localization-only mod

In the game, go to the save slot screen, and click on the Mods button (the wrench)

![](/images/translate/modsbutton.png)

Select "My Mods", then click Okay.

![](/images/translate/mymods.png)

Click the checkbox next to your mod and select "Play." (If you used the default settings, your mod's title will be "Untitled." You can change the title & icon by editing the `settings.xml` and `icon.png` files in the root directory of your mod.

![](/images/translate/selectmymod.png)

Click okay to confirm loading the mod

![](/images/translate/loadmod.png)

The title screen's lower right hand corner should indicate that the mod is indeed loaded. Any changes you have made will appear in the game now!

![](/images/translate/modtitlescreen.png)

Note that changes you make *after* you loaded the mod will not appear unless you go back to the title screen and click "reload mod." Then it will refresh and display those changes in game. To exit the mod, click "unload mod" or simply close the game.

##Step 2: Properly prepare compatible TSV files

You'll need to know how to create properly formatted TSV files in order for the game to correctly display them. There are two free tools I highly recommend:

[LibreOffice Calc](https://www.libreoffice.org/discover/calc/) (for importing / exporting TSV files)  
[Notepad++](https://notepad-plus-plus.org/) (for sanity checking the raw text)

I do not recommend Microsoft Excel as it has some trouble with properly creating UTF-8 TSV files, and you're likely to accidentally create corrupted output.

Once you've downloaded those two tools, you can get started. You should be able to open the game's TSV files directly in LibreOffice, just make sure to select "tab" as the proper delimeter.

When you're ready to export/save, follow these instructions:
https://github.com/larsiusprime/firetongue#exporting-tsv-files-from-libreoffice

##Step 3: How to convert an existing spreadsheet

Let's say you've already got a spreadsheet, and when you try to import it into LibreOffice as UTF-8 you get something like this:

![](/images/translate/fixencoding.png)

The little diamonds with "?" characters indicate that it's the wrong encoding. You can recover from this, but you *must* know which encoding was originally used to save the file. You also must select the correct language.
I happen to know this particular file I'm trying to open was written in Simplified Chinese and the encoding was [GB-18030](https://en.wikipedia.org/wiki/GB_18030), so I select those:

![](/images/translate/fixedencoding.png)

...and everything looks fine.

![](/images/translate/everythingisfine.png)

This should only happen to you if you neglect to choose UTF-8 as your encoding when saving the file. 

Remember:  
**!!!!!!ALWAYS USE UTF-8 to export!!!!!!**

So, when you save, be sure to [follow the Firetongue TSV export instructions](https://github.com/larsiusprime/firetongue#exporting-tsv-files-from-libreoffice) and all will be well for both loading in LibreOffice Calc and for using in game.

##Step 4: Optional -- manual inspection in Notepad++.

Here's an example of me doing things wrong. I've got chinese text in this document, and yet I'm using the default "Western Europe (Windows- 1252/WinLatin 1)" character set, and I'm including a quotation mark (`"`) as my text delimeter, when really it should be nothing.

![](/images/translate/exportbad.png)

This is going to break in all sorts of fun ways :)

Right click on the (bad) file and select "Edit with Notepad++"

![](/images/translate/corebadopen.png)

And sure enough...

![](/images/translate/corebad.png)

All the chinese characters have been replaced with "????" because the "Western Europe (Windows- 1252/WinLatin 1)" character set can't display them. There's literally nothing you can do to save this file at this point, it's been completely trashed, the Chinese information has
been forever lost, so you should keep a safe backup and probably not work directly from a TSV file, but instead a regular LibreOffice spreadsheet (ods) file.

If we select "Encoding" in Notepad++ we can see it thinks the encoding is "ANSI", which is totally wrong.

![](/images/translate/encoding.png)

Here's a properly exported TSV file:

![](/images/translate/coregood.png)

And selecting "Encoding" shows it's using UTF-8, which is correct.

![](/images/translate/utf8.png)

Another handy thing is to show the whitespace characters (space & tab).

![](/images/translate/showwhitespace.png)

This will reveal all the tabs and spaces. Remember, in TSV files tabs separate cells. So this can be a good way to check that everything looks as it should.

![](/images/translate/coregoodwhitespace.png)


And now you know how the Defender's Quest translation system works. Now you can change any text you want and have it immediately show up in the game.

For adding an entirely new language, some more instructions are required which I'll get to later.