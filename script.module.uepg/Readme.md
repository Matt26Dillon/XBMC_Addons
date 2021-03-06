![screenshot](https://github.com/Lunatixz/XBMC_Addons/raw/master/script.module.uepg/resources/images/icon.png)
# uEPG developed by Lunatixz

- Please only FORK TO IMPROVE. Nothing kills a project quicker then cloning and abuse of the GNU licence. This project was written to be universally used within Kodi. There is no need to fork for individual plugin use. Please respect the work and effort put into this project. Fork to contribute and/or improve the project only. Thank You = )

- [Support forum](https://forum.kodi.tv/showthread.php?tid=321231)
- [Report Issues](https://github.com/Lunatixz/XBMC_Addons/issues/new)

## About

- uEPG features easy Kodi plugin integration using either a listitem or json table. 
The EPG interface is fully customizable, includes genre colors, button tags (ex. "HD"), Favorite channel flagging and a programmable context menu.

## Controls:

- Navigate using `Up, Down, Left, Right, PageUp, PageDown`. Use `Select, Enter` or `OK` to play selected content. Toggle between fullscreen video and the EPG using `Back, Previous` or `Close`. Open the context menu using your specified context key. Exit the guide by `stopping` the currently playing video and pressing  `Back, Previous` or `Close` twice.

## Plugin Integration:

- ListItem option does not require (per channel parameters) but it is recommend. `channelname`,`channelnumber`,`channellogo` can be filled automatically using the listitems `Directory Names`,`Directory Range`,`Originating Plugin Icon`. Its recommend you include these parameters per item as a `listitem.property`. `starttime` can also automatically generate based on the current time and duration of each item (Not recommend for Live content).

### URL parameters:

- `skin_path` - Optional path for custom skin

- `refresh_interval` - How often uEPG should refresh guidedata (in Seconds).

- `refresh_path` - Path uEPG can use to retrieve updated guidedata (Not required for property type, instead include originating plugins path. EX. `plugin.video.ustvnow`).
 
- `json` - url quoted, json dump containing guidedata.

- `property` - `xbmcgui.Window(10000)` property name containing url quoted, json dump guidedata.

- `listitem` - plugin path that return guidedata listitems. Channels as `Directories`, individual programmes as `Links`. *note when a listitem parameter is unsupported ex. `starttime` follow `Custom Listitem parameter substitutions`.


#### URL parameter Examples:

- JSON

`xbmc.executebuiltin("RunScript(script.module.uepg,json=%s&refresh_path=%s&refresh_interval=%s)"%(urllib.quote_plus(json.dumps(USTVnow().uEPG())),urllib.quote_plus(json.dumps(sys.argv[0]+"?mode=20")),urllib.quote_plus(json.dumps("7200"))))`

- Property

`xbmc.executebuiltin("RunScript(script.module.uepg,property=%s&refresh_path=%s&refresh_interval=%s)"%(urllib.quote_plus("ustvnow_guidedata"),urllib.quote_plus(json.dumps(sys.argv[0])),urllib.quote_plus(json.dumps("7200”))))`

- ListItem

`xbmc.executebuiltin("RunScript(script.module.uepg,listitem=%s&refresh_path=%s&refresh_interval=%s)"%(urllib.quote_plus(sys.argv[0]+"?mode=20"),urllib.quote_plus(json.dumps(sys.argv[0])),urllib.quote_plus(json.dumps("7200”))))`

### Guidedata Parameters. 

- [Minimum JSON Example](https://github.com/Lunatixz/XBMC_Addons/raw/master/script.module.uepg/resources/example.json)

#### Per channel parameters:

- `channelname`,`channelnumber`,`channellogo`

- `isfavorite` - Optional channel favorite flag

- `guidedata`  - List of individual programme elements.

#### Minimum programme parameters:

- `starttime` - seconds in epoch.

- `url` or `path` - play path

- `label` or `title`

- `runtime` or `duration` - in seconds.

- `label2` - Optional EPG tag ex. “HD”

- `thumb`  - Optional but should be included.

#### Extended programme parameters:

- [ListItem parameter details](https://codedocs.xyz/xbmc/xbmc/group__python__xbmcgui__listitem.html#ga0b71166869bda87ad744942888fb5f14)

- [ListItem Art parameter details](https://codedocs.xyz/xbmc/xbmc/group__python__xbmcgui__listitem.html#gad3f9b9befa5f3d2f4683f9957264dbbe)

- [ListItem StreamDetails parameter details](https://codedocs.xyz/xbmc/xbmc/group__python__xbmcgui__listitem.html#gaf0c020ba8bc205d61e786dfec9111cdc)

#### Listitem parameter examples:

- Kodi file parameters 
`["title","artist","albumartist","genre","year","rating","album","track","duration","comment","lyrics","musicbrainztrackid","musicbrainzartistid","musicbrainzalbumid","musicbrainzalbumartistid","playcount","fanart","director","trailer","tagline","plot","plotoutline","originaltitle","lastplayed","writer","studio","mpaa","cast","country","imdbnumber","premiered","productioncode","runtime","set","showlink","streamdetails","top250","votes","firstaired","season","episode","showtitle","thumbnail","file","resume","artistid","albumid","tvshowid","setid","watchedepisodes","disc","tag","art","genreid","displayartist","albumartistid","description","theme","mood","style","albumlabel","sorttitle","episodeguide","uniqueid","dateadded","size","lastmodified","mimetype","specialsortseason","specialsortepisode"]`

- Kodi art parameters  
`["thumb","poster","fanart","banner","landscape","clearart","clearlogo"]`

- Kodi pvr parameters  
`["title","plot","plotoutline","starttime","endtime","runtime","progress","progresspercentage","genre","episodename","episodenum","episodepart","firstaired","hastimer","isactive","parentalrating","wasactive","thumbnail","rating","originaltitle","cast","director","writer","year","imdbnumber","hastimerrule","hasrecording","recording","isseries"]`

#### Custom Listitem parameter substitutions
`'comment' = json.dumps({"channelname":"name","channelnumber":number,"channellogo":"logo","label":"title","label2":"HD","startime":startime}))`

## Customize Skin:

### Properties:

`$INFO[Window(10000).Property(PluginName)]` - Originating plugin meta 

`$INFO[Window(10000).Property(PluginIcon)]` - Originating plugin meta 

`$INFO[Window(10000).Property(pluginAuthor)]` - Originating plugin meta 

`$INFO[Window(10000).Property(Time)` - Focused show time range ex: `5:00PM-6:00PM`

#### Hard Coded Control Settings:

`<onload>SetProperty(uEPG.rowCount,5,10000)</onload>` - EPG row count

`<onload>SetProperty(uEPG.timeCount,3,10000)</onload>` - EPG time row count, ie. 3 = `12:00  12:30  1:00`

`<onload>SetProperty(uEPG.textColor,0xFFFFFFFF,10000)</onload>` - EPG Text Color

`<onload>SetProperty(uEPG.disabledColor,0xFFFFFFFF,10000)</onload>` - EPG No Focus Color

`<onload>SetProperty(uEPG.focusedColor,0xFFFFFFFF,10000)</onload>` - EPG Focus Color

`<onload>SetProperty(uEPG.shadowColor,0xFF000000,10000)</onload>` - EPG Shadow Color

`<onload>SetProperty(uEPG.pastColor,0xFF0f85a5,10000)</onload>` - EPG Past Fade Color

`<onload>SetProperty(uEPG.futureColor,0xFF0f85a5,10000)</onload>` - EPG Future Fade Color

`<onload>SetProperty(uEPG.textFont,font12,10000)</onload>` - EPG Font

### Controls:

`Container(40000)` - Listitem Container ex `$INFO[Container(40000).ListItem.Title]`

### Textures:

#### Hard Coded Images:

`epg-genres\COLOR_ButtonNoFocus.png` - EPG No Focus, and respective genre colors (see default skin for example). 

`ButtonFocus.png` - EPG Focus

`TimeBar.png`  - EPG Time Bar

`PastFade.png` - EPG Past Fade

`FutureFade.png` - EPG Future Fade

More details to come...
