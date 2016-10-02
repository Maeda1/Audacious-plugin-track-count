# Audacious-plugin-track-count
For Linux.
In addition to existing Audacious's "track change" plugin, it keep count and history of played files, and display informations in a popup when track changes.
Display are in english or french (depending on current system locale).

##Needs / prerequisites
It needs :
- *ssv_ziks1* and *ssv_ziks2*, and make them executable with *chmod +x*
- **Audacious** (of course :)).
- The **audacious-plugins** package (it include the "song change" plugin that we need).
- Enabling the *song change* plugin in Audacious, with following settings :
 - *When a track starts* : put the full path of ssv_ziks1 location
 - *When a track ends* : put the full path of ssv_ziks2 location
- notify-send from the **libnotify** package

**/!\ Please put what you want in the settings of Audacious, under *Playlist*, *Custom string display* as all this plugin will keep and compare tags of songs as set in this field. Don't change anything after beginning to use ssv_ziks1 and ssv_ziks2 because it will NOT find previous tracks, because track name (as defined in *Custom string display* has changed. Choose and keep the *Custom string display* one and for all. If you need to change it, you will have to make changes in the *play_count* file too !/!\**

Keep in mind that :
- all your tags should be correctly set on your tracks.
- your *Custom string display* should be created in order to have an unique string for each tracks, then include track number, album, author, and track name, and all informations that you want to make it unique.

##How it works ?
- A file in *~/.audacious/* named *play_count* will contain all the database of (fully) played files.
- When a track begins to play in Audacious, *song change* plugin will execute *ssv_ziks1* : it writes in */tmp/zik_actuelle* the text as defined in Audacious's settings *Custom string display*.
- When the track ends to play in Audacious, *song change* plugin will execute *ssv_ziks2* : it writes informations of the track (as defined in *Custom string display*) along with date / time and check if it has already be played before, if it founds it in *play_count* file, it increases the count by one.
- In the display popup, you have a notation system that takes the play counts of current track file and the lengh of that file. The listen time is displayed too, and if it reaches some hours value, it display a star or better, a heart symbol :). First grade is a star, then when you reaches five stars, the next step is one heart, until five hearts !

##Known bugs :
- You should not make use of following string in your audio file tags : 
 - ~
 - [ *or* ]
 - /
 - \
