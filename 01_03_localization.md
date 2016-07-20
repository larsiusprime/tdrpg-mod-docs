##1.3 Text & Localization

Throughout the game's data files you'll see stuff like this:

```xml
<pearl id="0" level="$INDEX_1_1_WHERE_AM_I_TITLE" level_id="1_1_where_am_i" description="$INDEX_1_1_WHERE_AM_I_TEXT" _x="70" _y="90" _type="battle"/>
```

Where you might have expected something like this:

```xml
<pearl id="0" level="The Half-Way World" level_id="1_1_where_am_i" description="Lost and alone, $MCG finds herself caught between life and death." _x="70" _y="90" _type="battle"/>
```

That's because Defender's Quest is thoroughly [localized](https://en.wikipedia.org/wiki/Internationalization_and_localization) and very few human-readable strings are presented directly to the user.

Instead, bits of text are stored as *reference flags* like `"$INDEX_WHERE_AM_I_TITLE"`, which simply means "the title of the level 1_1_where_am_i, in whatever the current language is, and which resolves to "The Half-Way World" in English.

Defender's Quest uses the open source localization framework [Firetongue](http://github.com/larsiusprime/firetongue), which provides further documentation.
