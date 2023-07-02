---
sidebar_position: 3
---

# Rest API

Some commands may be invoked using Rest_api interface.

From a device on the same network, you can use

```
curl volumio.local/api/v1/commands/mycommand

```

Where _volumio.local_ is the device to be reached. You can also use the IP adress instead.

From the device itself (via a keyboard plugged into it or through [SSH](https://volumio.github.io/docs/User_Manual/SSH.html)), use :

```
curl localhost:3000/api/v1/commands/mycommand

```

REST APIs can be also invoked trough the network, for example (assuming Volumio's IP is 192.168.1.22):

```
curl http://192.168.1.22/api/v1/commands/mycommand

```

And of course, _mycommand_ is to be replaced by the command to be used. (see below)


## Available commands

### Playback commands

All API calls will look like:

```
volumio.local/api/v1/commands/?cmd=
```

example:

```
volumio.local/api/v1/commands/?cmd=play
```

Available commands:

### Playback

* Play
```
volumio.local/api/v1/commands/?cmd=play&N=2
```
where N is optional and is the ordinal number of the track in the queue you wish to start to play from. The above call will play the third track in the queue.

* Toggle between play and pause
```
volumio.local/api/v1/commands/?cmd=toggle
```
* Stop
```
volumio.local/api/v1/commands/?cmd=stop
```

* Pause
```
volumio.local/api/v1/commands/?cmd=pause
```

* Previous
```
volumio.local/api/v1/commands/?cmd=prev
```

* Next
```
volumio.local/api/v1/commands/?cmd=next
```

* Volume
```
volumio.local/api/v1/commands/?cmd=volume&volume=80
```
where volume can be: mute, unmute, plus, minus (plus and minus will increase\decrease as per parameter one click volume steps)

### Music Library

* Get the current state of the player
```
volumio.local/api/v1/getState
```

Response
```json
{
    "status": "play",
    "position": 2,
    "title": "Shine On You Crazy Diamond (Part 1-5))",
    "artist": "Pink Floyd",
    "album": "Wish You Were Here (24Bit/96KHz)",
    "albumart": "/albumart?cacheid=955&web=Pink%20Floyd/Wish%20You%20Were%20Here%20(24Bit%2F96KHz)/extralarge&path=%2FNAS%2FFLAC%2FPink%20Floyd%20-%20Wish%20You%20Were%20Here%20(24-96)&metadata=false",
    "uri": "mnt/NAS/FLAC/Pink Floyd - Wish You Were Here (24-96)/1 - Shine On You Crazy Diamond (Part 1).flac",
    "trackType": "flac",
    "seek": 53057,
    "duration": 809,
    "samplerate": "96 kHz",
    "bitdepth": "24 bit",
    "channels": 2,
    "random": false,
    "repeat": false,
    "repeatSingle": false,
    "consume": false,
    "volume": 43,
    "disableVolumeControl": false,
    "mute": false,
    "stream": "flac",
    "updatedb": false,
    "volatile": false,
    "service": "mpd"
}
```

* Get the playback queue
```
volumio.local/api/v1/getQueue
```

Response
```json
{"queue":
  [
    {
        "uri": "mnt/NAS/FLAC/Bob Dylan The Best Of Remastered 1997 [EAC-FLAC](oan)/03 - Don't Think Twice, It's All Right.flac",
        "service": "mpd",
        "name": "Don't Think Twice, It's All Right",
        "artist": "Bob Dylan",
        "album": "The Best Of",
        "type": "track",
        "tracknumber": 0,
        "albumart": "/albumart?cacheid=955&web=Bob%20Dylan/The%20Best%20Of/extralarge&path=%2FNAS%2FFLAC%2FBob%20Dylan%20The%20Best%20Of%20Remastered%201997%20%5BEAC-FLAC%5D(oan)&metadata=false",
        "duration": 221,
        "samplerate": "44.1 kHz",
        "bitdepth": "16 bit",
        "trackType": "flac",
        "channels": 2
    },
    {
        "uri": "mnt/NAS/FLAC/DooBop - hdtracks/2-The DooBop Song.flac",
        "service": "mpd",
        "name": "The Doo-Bop Song",
        "artist": "Miles Davis",
        "album": "Doo-Bop",
        "type": "track",
        "tracknumber": 0,
        "albumart": "/albumart?cacheid=955&web=Miles%20Davis/Doo-Bop/extralarge&path=%2FNAS%2FFLAC%2FDooBop%20-%20hdtracks&metadata=false",
        "duration": 307,
        "samplerate": "192 kHz",
        "bitdepth": "24 bit",
        "trackType": "flac",
        "channels": 2
    },
    {
        "uri": "mnt/NAS/FLAC/Pink Floyd - Wish You Were Here (24-96)/1 - Shine On You Crazy Diamond (Part 1).flac",
        "service": "mpd",
        "name": "Shine On You Crazy Diamond (Part 1-5))",
        "artist": "Pink Floyd",
        "album": "Wish You Were Here (24Bit/96KHz)",
        "type": "track",
        "tracknumber": 0,
        "albumart": "/albumart?cacheid=955&web=Pink%20Floyd/Wish%20You%20Were%20Here%20(24Bit%2F96KHz)/extralarge&path=%2FNAS%2FFLAC%2FPink%20Floyd%20-%20Wish%20You%20Were%20Here%20(24-96)&metadata=false",
        "duration": 809,
        "samplerate": "96 kHz",
        "bitdepth": "24 bit",
        "trackType": "flac",
        "channels": 2
    }
  ]
}
```

* Clear the queue
```
volumio.local/api/v1/commands/?cmd=clearQueue
```

* List Playlists
```
volumio.local/api/v1/listplaylists
```
* Play a Playlist
```
volumio.local/api/v1/commands/?cmd=playplaylist&name=Rock
```
Where name is the name of the playlist to play

* Repeat a track
```
volumio.local/api/v1/commands/?cmd=repeat&value=key
```
Where key is _true_ or _false_; if value is absent it toggles.

* Random Makes the order in which tracks are played random
```
volumio.local/api/v1/commands/?cmd=random&value=key
```
Where key is _true_ or _false_; if value is absent it toggles.

### Browsing

* Browse

```
volumio.local/api/v1/browse?uri=uri
```

Where uri is the uri we want to browse. If not specified, it will start from root (/)

Response
```json
{
    "navigation": {
        "lists": [
            {
                "albumart": "/albumart?sourceicon=music_service/mpd/favouritesicon.png",
                "name": "Favorites",
                "uri": "favourites",
                "plugin_type": "",
                "plugin_name": ""
            },
            {
                "albumart": "/albumart?sourceicon=music_service/mpd/playlisticon.png",
                "name": "Playlists",
                "uri": "playlists",
                "plugin_type": "music_service",
                "plugin_name": "mpd"
            },
            {
                "albumart": "/albumart?sourceicon=music_service/mpd/musiclibraryicon.png",
                "name": "Music Library",
                "uri": "music-library",
                "plugin_type": "music_service",
                "plugin_name": "mpd"
            },
            {
                "albumart": "/albumart?sourceicon=music_service/mpd/artisticon.png",
                "name": "Artists",
                "uri": "artists://",
                "plugin_type": "music_service",
                "plugin_name": "mpd"
            },
            {
                "albumart": "/albumart?sourceicon=music_service/mpd/albumicon.png",
                "name": "Albums",
                "uri": "albums://",
                "plugin_type": "music_service",
                "plugin_name": "mpd"
            },
            {
                "albumart": "/albumart?sourceicon=music_service/mpd/genreicon.png",
                "name": "Genres",
                "uri": "genres://",
                "plugin_type": "music_service",
                "plugin_name": "mpd"
            },
            {
                "name": "Media Servers",
                "uri": "upnp",
                "plugin_type": "music_service",
                "plugin_name": "upnp_browser",
                "albumart": "/albumart?sourceicon=music_service/upnp_browser/dlnaicon.png"
            },
            {
                "albumart": "/albumart?sourceicon=music_service/last_100/icon.png",
                "name": "last 100",
                "uri": "Last_100",
                "plugin_type": "music_service",
                "plugin_name": "last_100"
            },
            {
                "albumart": "/albumart?sourceicon=music_service/webradio/icon.png",
                "icon": "fa fa-microphone",
                "name": "Web Radio",
                "uri": "radio",
                "plugin_type": "music_service",
                "plugin_name": "webradio"
            },
            {
                "albumart": "/albumart?sourceicon=music_service/tunein_radio/tunein.svg ",
                "icon": "fa fa-microphone",
                "name": "TuneIn Radio",
                "uri": "tunein",
                "plugin_type": "music_service",
                "plugin_name": "tunein_radio"
            },
            {
                "name": "TIDAL",
                "uri": "tidal://",
                "plugin_type": "music_service",
                "plugin_name": "streaming_services",
                "albumart": "/albumart?sourceicon=music_service/streaming_services/icons/tidal/tidal-icon.png"
            }
        ]
    }
}
```

If for example we now want to browse "Web Radio", uri will be "radio", and our query will be:

```
volumio.local/api/v1/browse?uri=radio
```

IMPORTANT: The value albumart is a relative path. So, it must be handled this way:
* If albumart value starts with http, then no further operation is needed and the resulting url will show an albumart
* Otherwise, prepend the string formed by: http:// + IP ADDRESS of Volumio device. Example: http://192.168.1.22/albumart?sourceicon=music_service/webradio/icon.png

FILTERING

To improve navigation, especially on clients with limited memory or computing power,
_filters_ can be applied to reduce the number of items returned by a query.
The available filter methods are:
* limit : limit the response to N elements
* offset : start from element N in a list

When filtering is applied, a new "count" field is populated with the total number of items availble and a new filter field is added, which shows active filters in the query.

Example: To show only 2 elements, starting from the second element:

```
volumio.local/api/v1/browse?uri=music-library/NAS/FLAC&limit=2&offset=2
```

Response
```json
{
  "navigation": {
    "prev": {
      "uri": "music-library/NAS"
    },
    "lists": [
      {
        "availableListViews": [
          "grid",
          "list"
        ],
        "items": [
          {
            "service": "mpd",
            "type": "song",
            "title": "Tchaikovsky:Hopak from Mazeppa",
            "artist": "The Minnesota Orchestra",
            "album": "Exotic Dances From The Opera",
            "uri": "music-library/NAS/FLAC/macrodinamica_Tchaikovsky Hopak.flac",
            "albumart": "/albumart?cacheid=867&path=%2Fmnt%2FNAS%2FFLAC&icon=music&metadata=false"
          },
          {
            "type": "folder",
            "title": "[EAC FLAC CUE] Nomadi - Ma Noi No!",
            "service": "mpd",
            "albumart": "/albumart?cacheid=867&path=%2Fmnt%2FNAS%2FFLAC%2F%5BEAC%20FLAC%20CUE%5D%20Nomadi%20-%20Ma%20Noi%20No!&icon=folder-o&metadata=false",
            "uri": "music-library/NAS/FLAC/[EAC FLAC CUE] Nomadi - Ma Noi No!"
          }
        ],
        "count": 194,
        "filters": {
          "offset": 2,
          "limit": 2
        }
      }
    ]
  }
}
```


* Search

```
volumio.local/api/v1/search?query=searchquery
```

Where searchquery is the search query we want to perform (it is suggested to send it urlencoded)


Response
```json
{
    "navigation": {
        "isSearchResult": true,
        "lists": [
            {
                "title": "Found 1 Artist 'paolo'",
                "availableListViews": [
                    "list",
                    "grid"
                ],
                "items": [
                    {
                        "service": "mpd",
                        "type": "folder",
                        "title": "Paolo Conte",
                        "uri": "artists://Paolo%20Conte",
                        "albumart": "/albumart?cacheid=955&web=Paolo%20Conte//extralarge&icon=users"
                    }
                ]
            },
            {
                "title": "Found 1 Album 'paolo'",
                "availableListViews": [
                    "list",
                    "grid"
                ],
                "items": [
                    {
                        "service": "mpd",
                        "type": "folder",
                        "title": "Paolo Conte",
                        "artist": "",
                        "album": "",
                        "uri": "albums:///Paolo%20Conte",
                        "albumart": "/albumart?cacheid=955&web=/Paolo%20Conte/extralarge&path=%2Fmnt%2FNAS%2FFLAC%2FPaolo%20Conte%20-%201984%20-%20Paolo%20Conte%20%5B1995%20Reissue%5D&icon=fa-tags&metadata=false"
                    }
                ]
            },
            {
                "title": "Web Radio",
                "icon": "fa icon",
                "availableListViews": [
                    "list"
                ],
                "items": [
                    {
                        "service": "webradio",
                        "type": "webradio",
                        "title": "RADIO.DISCOunt",
                        "artist": "",
                        "album": "",
                        "uri": "http://yp.shoutcast.com/sbin/tunein-station.m3u?id=99242899",
                        "albumart": "http://i.radionomy.com/document/radios/b/b398/b398d972-1ca0-426e-a6af-c23f86033bb7.jpg"
                    },
                    {
                        "service": "webradio",
                        "type": "webradio",
                        "title": "Whippet Radio",
                        "artist": "",
                        "album": "",
                        "uri": "http://yp.shoutcast.com/sbin/tunein-station.m3u?id=1629210",
                        "icon": "fa fa-microphone"
                    },
                    {
                        "service": "webradio",
                        "type": "webradio",
                        "title": "Radio FlyWeb",
                        "artist": "",
                        "album": "",
                        "uri": "http://yp.shoutcast.com/sbin/tunein-station.m3u?id=1613271",
                        "albumart": "http://i.radionomy.com/document/radios/9/9721/9721b1a4-b10e-43b7-98cf-087245fda05e.jpg"
                    },
                    {
                        "service": "webradio",
                        "type": "webradio",
                        "title": "musicfactorystudio1",
                        "artist": "",
                        "album": "",
                        "uri": "http://yp.shoutcast.com/sbin/tunein-station.m3u?id=1817423",
                        "albumart": "http://i.radionomy.com/documents/radio/15362339-b029-4abd-a5b0-e8e898f8a22e.s165.png"
                    },
                    {
                        "service": "webradio",
                        "type": "webradio",
                        "title": "Radio San Paolo by DeSaLeo",
                        "artist": "",
                        "album": "",
                        "uri": "http://yp.shoutcast.com/sbin/tunein-station.m3u?id=920919",
                        "albumart": "http://i.radionomy.com/documents/radio/9a4389b5-7a6d-4094-8b7e-9d559b343839.s165.png"
                    }
                ]
            }
        ]
    }
}
```

### Adding items to playback

Items can be added to playback in 3 ways:
* Replacing the current content of the queue and playing Items (default and suggested)
* Adding Items to queue and playing the items (so queue will not be cleared)
* Adding items to queue


* Replace the current content of the queue

POST
```
volumio.local/api/v1/replaceAndPlay
```

Payload
```json
{
  "item": {
    "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/06 - Forget It.flac",
    "service": "mpd",
    "title": "Forget It",
    "artist": "Rodriguez",
    "album": "Cold Fact",
    "type": "song",
    "tracknumber": 0,
    "duration": 110,
    "trackType": "flac"
  },
  "list": [
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/01 - Sugar Man.flac",
      "service": "mpd",
      "title": "Sugar Man",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 229,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/02 - Only Good for Conversation.flac",
      "service": "mpd",
      "title": "Only Good for Conversation",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 144,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/03 - Crucify Your Mind.flac",
      "service": "mpd",
      "title": "Crucify Your Mind",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 152,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/04 - This Is Not a Song, It's an Outburst- Or, The Establishment Blues.flac",
      "service": "mpd",
      "title": "This Is Not a Song, It's an Outburst: Or, The Establishment Blues",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 127,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/05 - Hate Street Dialogue.flac",
      "service": "mpd",
      "title": "Hate Street Dialogue",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 154,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/06 - Forget It.flac",
      "service": "mpd",
      "title": "Forget It",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 110,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/07 - Inner City Blues.flac",
      "service": "mpd",
      "title": "Inner City Blues",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 207,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/08 - I Wonder.flac",
      "service": "mpd",
      "title": "I Wonder",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 154,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/09 - Like Janis.flac",
      "service": "mpd",
      "title": "Like Janis",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 156,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/10 - Gommorah (A Nursery Rhyme).flac",
      "service": "mpd",
      "title": "Gommorah (A Nursery Rhyme)",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 141,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/11 - Rich Folks Hoax.flac",
      "service": "mpd",
      "title": "Rich Folks Hoax",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 186,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/12 - Jane S. Piddy.flac",
      "service": "mpd",
      "title": "Jane S. Piddy",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 180,
      "trackType": "flac"
    }
  ],
  "index": 5
}
```

Where
* `List`: is the list of object we want to play
* `Index`: is the item we want to play first (in this example we are starting playback from track 6)
* `Item`: is the selected item that will play first

Alternatively, a single item can be provided (in this case, put directly the item in the payload, without using the values index, list and item)

* Adding items to queue

POST
```
volumio.local/api/v1/addToQueue
```

Payload
```json
[
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/01 - Sugar Man.flac",
      "service": "mpd",
      "title": "Sugar Man",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 229,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/02 - Only Good for Conversation.flac",
      "service": "mpd",
      "title": "Only Good for Conversation",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 144,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/03 - Crucify Your Mind.flac",
      "service": "mpd",
      "title": "Crucify Your Mind",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 152,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/04 - This Is Not a Song, It's an Outburst- Or, The Establishment Blues.flac",
      "service": "mpd",
      "title": "This Is Not a Song, It's an Outburst: Or, The Establishment Blues",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 127,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/05 - Hate Street Dialogue.flac",
      "service": "mpd",
      "title": "Hate Street Dialogue",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 154,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/06 - Forget It.flac",
      "service": "mpd",
      "title": "Forget It",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 110,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/07 - Inner City Blues.flac",
      "service": "mpd",
      "title": "Inner City Blues",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 207,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/08 - I Wonder.flac",
      "service": "mpd",
      "title": "I Wonder",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 154,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/09 - Like Janis.flac",
      "service": "mpd",
      "title": "Like Janis",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 156,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/10 - Gommorah (A Nursery Rhyme).flac",
      "service": "mpd",
      "title": "Gommorah (A Nursery Rhyme)",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 141,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/11 - Rich Folks Hoax.flac",
      "service": "mpd",
      "title": "Rich Folks Hoax",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 186,
      "trackType": "flac"
    },
    {
      "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/12 - Jane S. Piddy.flac",
      "service": "mpd",
      "title": "Jane S. Piddy",
      "artist": "Rodriguez",
      "album": "Cold Fact",
      "type": "song",
      "tracknumber": 0,
      "duration": 180,
      "trackType": "flac"
    }
  ]
```
Just send an array with all the items you want to be added to queue.


* Adding items and playing them without clearing the queue
POST
```
volumio.local/api/v1/addToQueue
```

Payload
```json
{
  "uri": "music-library/NAS/HI_Res_Music/Rodriguez - 1970 - Cold Fact [Light in the Attic, LITA036]/12 - Jane S. Piddy.flac",
  "service": "mpd",
  "title": "Jane S. Piddy",
  "artist": "Rodriguez",
  "album": "Cold Fact",
  "type": "song",
  "tracknumber": 0,
  "duration": 180,
  "trackType": "flac"
}
```
Just send an item or an items array with all the items you want to be added to queue.

* Collection Statistics

```
volumio.local/api/v1/collectionstats
```

This API returns counts and play length of the music collection currently handled by Volumio


Response
```json
{
    "artists": 3,
    "albums": 4,
    "songs": 105,
    "playtime": "7:11:15"
}
```

* Zones

```
volumio.local/api/v1/getzones
```

This API returns a list of all Volumio devices in a given network, complete with now playing data.


Response
```json
{"zones":
  [
    {
        "id": "b1050de4-4702-4fb1-a495-8bc312854060",
        "host": "http://192.168.211.1",
        "name": "Volumio",
        "isSelf": true,
        "state": {
            "status": "stop",
            "volume": 43,
            "mute": false,
            "artist": "",
            "track": "",
            "albumart": "http://192.168.211.1/albumart"
        }
    },
    {
        "id": "b1050de4-4702-4fb1-a495-8asds4060",
        "host": "http://192.168.1.22",
        "name": "Volumio Studio",
        "isSelf": false,
        "state": {
            "status": "stop",
            "volume": 43,
            "mute": false,
            "artist": "",
            "track": "",
            "albumart": "http://192.168.1.22/albumart"
        }
    }
  ]
}
```

IMPORTANT: If isSelf = true, it means that this is the device that handled the REST call.


### Notifications

Volumio REST API can be used in an event driven fashion. Volumio can notify via POST calls when state changes. This is a much more efficient and elegant way to retrieve informations, instead of continuously polling the relevant endpoints.

For example, we can ask Volumio to notify every status change to the URL http://192.168.1.33/volumiostatus (the URL is totally configurable, just make sure it is a valid http endpoint).
To do so, we will simply make the POST request:

### POST
```
volumio.local/api/v1/pushNotificationUrls?url=http://192.168.1.33/volumiostatus
```

Body

```
{"url":"http://192.168.1.33/volumiostatus"}
```

Response
```json
{
    "success": true
}
```
NOTE: Multiple endpoints can be added.

We can now check if our URL has been added properly, by issuing this GET request:

```
volumio.local/api/v1/pushNotificationUrls
```

Response
```json
["http://192.168.1.33/volumiostatus"]
```

If we want, we can issue a DELETE request to remove our endpoint:

```
volumio.local/api/v1/pushNotificationUrls?url=http://192.168.1.33/volumiostatus
```

When we've added our notification url, we will receive notifications everytime something in Volumio playback system changes.
There are multiple events that trigger a notification:
* state : when playback status changes
* queue: when playback status changes
* zones: when zone status changes

EXAMPLE:

```
{ item: "state",
    data:
    { status: "play",
        position: 3,
        title: "WIsh You Were Here",
        artist: "Pink Floyd",
        album: "Wish You Were Here (24Bit/96KHz)",
        albumart: "/albumart?cacheid=955&web=Pink%20Floyd/Wish%20You%20Were%20Here%20(24Bit%2F96KHz)/extralarge&path=%2FNAS%2FFLAC%2FPink%20Floyd%20-%20Wish%20You%20Were%20Here%20(24-96)&metadata=false",
        uri: "mnt/NAS/FLAC/Pink Floyd - Wish You Were Here (24-96)/4 - Wish You Were Here.flac",
        trackType: "flac",
        seek: 336,
        duration: 336,
        samplerate: "96 kHz",
        bitdepth: "24 bit",
        channels: 2,
        random: false,
        repeat: false,
        repeatSingle: false,
        consume: false,
        volume: 42,
        disableVolumeControl: false,
        mute: false,
        stream: "flac",
        updatedb: false,
        volatile: false,
        service: "mpd" } }
```

```
{ item: "queue",
    data:
    [ { uri: "mnt/NAS/FLAC/Bob Dylan The Best Of Remastered 1997 [EAC-FLAC](oan)/03 - Don\"t Think Twice, It\"s All Right.flac",
        service: "mpd",
        name: "Don\"t Think Twice, It\"s All Right",
        artist: "Bob Dylan",
        album: "The Best Of",
        type: "track",
        tracknumber: 0,
        albumart: "/albumart?cacheid=955&web=Bob%20Dylan/The%20Best%20Of/extralarge&path=%2FNAS%2FFLAC%2FBob%20Dylan%20The%20Best%20Of%20Remastered%201997%20%5BEAC-FLAC%5D(oan)&metadata=false",
        duration: 221,
        samplerate: "44.1 kHz",
        bitdepth: "16 bit",
        trackType: "flac",
        channels: 2 },
        { uri: "mnt/NAS/FLAC/DooBop - hdtracks/2-The DooBop Song.flac",
            service: "mpd",
            name: "The Doo-Bop Song",
            artist: "Miles Davis",
            album: "Doo-Bop",
            type: "track",
            tracknumber: 0,
            albumart: "/albumart?cacheid=955&web=Miles%20Davis/Doo-Bop/extralarge&path=%2FNAS%2FFLAC%2FDooBop%20-%20hdtracks&metadata=false",
            duration: 307,
            samplerate: "192 kHz",
            bitdepth: "24 bit",
            trackType: "flac",
            channels: 2 },
        { uri: "mnt/NAS/FLAC/Pink Floyd - Wish You Were Here (24-96)/1 - Shine On You Crazy Diamond (Part 1).flac",
            service: "mpd",
            name: "Shine On You Crazy Diamond (Part 1-5))",
            artist: "Pink Floyd",
            album: "Wish You Were Here (24Bit/96KHz)",
            type: "track",
            tracknumber: 0,
            albumart: "/albumart?cacheid=955&web=Pink%20Floyd/Wish%20You%20Were%20Here%20(24Bit%2F96KHz)/extralarge&path=%2FNAS%2FFLAC%2FPink%20Floyd%20-%20Wish%20You%20Were%20Here%20(24-96)&metadata=false",
            duration: 809,
            trackType: "flac" },
        { uri: "mnt/NAS/FLAC/Pink Floyd - Wish You Were Here (24-96)/4 - Wish You Were Here.flac",
            service: "mpd",
            name: "WIsh You Were Here",
            artist: "Pink Floyd",
            album: "Wish You Were Here (24Bit/96KHz)",
            type: "track",
            tracknumber: 0,
            albumart: "/albumart?cacheid=955&web=Pink%20Floyd/Wish%20You%20Were%20Here%20(24Bit%2F96KHz)/extralarge&path=%2FNAS%2FFLAC%2FPink%20Floyd%20-%20Wish%20You%20Were%20Here%20(24-96)&metadata=false",
            duration: 336,
            samplerate: "96 kHz",
            bitdepth: "24 bit",
            trackType: "flac",
            channels: 2 },
        { uri: "mnt/NAS/FLAC/Red Hot Chili Peppers - Blood Sugar Sex Magik [FLAC]/04 - Funky Monks.flac",
            service: "mpd",
            name: "Funky Monks",
            artist: "Red Hot Chili Peppers",
            album: "Blood Sugar Sex Magik",
            type: "track",
            tracknumber: 0,
            albumart: "/albumart?cacheid=955&web=Red%20Hot%20Chili%20Peppers/Blood%20Sugar%20Sex%20Magik/extralarge&path=%2FNAS%2FFLAC%2FRed%20Hot%20Chili%20Peppers%20-%20Blood%20Sugar%20Sex%20Magik%20%5BFLAC%5D&metadata=false",
            duration: 323,
            trackType: "flac" } ] }
```

### System Utilities

* Ping

```
volumio.local/api/v1/ping
```

This API simply replies to the ping request, to signal activity.


Response
```
pong
```

* Get system version



```
volumio.local/api/v1/getSystemVersion
```

This API provides the software version, build date and hardware informations.


Response
```
{"systemversion":"2.632","builddate":"Thu Oct  3 21:47:57 CEST 2019","variant":"volumio","hardware":"pi"}
```

* Get system informations



```
volumio.local/api/v1/getSystemInfo
```

This API provides summary information of the device, the service name and playback status.


Response
```
{
  "id": "b8507fe7-dc48-40df-8ef4-4d0fff88dc05",
  "host": "http://192.168.1.126",
  "name": "Volumio5",
  "type": "device",
  "serviceName": "Volumio",
  "state": {
    "status": "play",
    "volume": 40,
    "mute": false,
    "artist": "Al Green",
    "track": "Back Up Train",
    "albumart": "http://192.168.1.126/albumart?cacheid=7&web=Al%20Green/Anthology%20(Disc%201)/extralarge&path=%2FNAS%2FHi_Res%2FAl%20Green%20-%20Anthology%20-%204CD-Set%20(1997)%20%5BFLAC%5D%20TG%2FAnthology%20(Disc%201)%20(1997)%20%5BFLAC%5D&metadata=false"
  },
  "systemversion": "2.803",
  "builddate": "Tue Jul 28 21:28:37 CEST 2020",
  "variant": "volumio",
  "hardware": "pi"
}
```

### Tiny Albumart Facility

Volumio provides an alternative facility to retrieve albumarts with shorter URLs. This is especially useful in situations where the client cannot handle large albumarts or
the full length url with its url encoding of albumart.
PLEASE NOTE: Tinyalbumart only fetches albumart for artists and albums from online datastores (no local albumart will be retrieved).

* Artist Art

```
volumio.local/tinyart/the_beatles/large
```

* IMPORTANT: Replace all spaces in the artist name with _ .
* Size is the last url parameter. For artist it can be only large (300x300px)

* Album art

```
volumio.local/tinyart/the_beatles/abbey_road/large
```

* IMPORTANT: Replace all spaces in the artist name  and album name with _ .
* Size is the last url parameter. For albums it can be: small (34x34px), medium (64x64px), large (174x174px), extralarge (300x300px)

* Sourceicon

```
volumio.local/tinyart/?sourceicon=music_service/mpd/favouritesicon.png
```


### Metadatas (premium)

Volumio offers the possibility to retrieve rich metadata for artists, albums, tracks and much more.

:::tip
This feature is available only for users with an active Premium or Superstar subscription. The API is designed in a way that requests will be successful if user has an appropriate account and fail otherwise.
:::

#### Base Url

The base URL is identical for all metadata REST Calls. It is made up by the backend IP address and `/api/v1/pluginEndpoint`

```
http://192.168.1.23/api/v1/pluginEndpoint
```

This is a POST call and URL is the same for every kind of request. What changes is the payload, example:

```json
{
  "endpoint": "metavolumio",
  "data": {
    "mode": "storyArtist",
    "artist": "Pink Floyd"
  }
}
```


If the call is successful, you'll see something like in the response:

```json
{
    "success": true,
    "data": {
        "type": "story",
        "value": "Pink Floyd were an English rock band formed in London in 1964..."
    }
}
```

NOTE: The metadatas are shown in the language that user has set. This information is automatically obtained by Volumio backend. In case a localized information is not found, the english version will be delivered.

Else, if the metadata cannot be obtained, or the user does not have a required premium account, response will be like:

```json
{
    "success": false,
    "error": "Metavolumio not available"
}
```

#### Artist Story

Retrieves the Artist's Biography

Payload:


```json
{
  "endpoint": "metavolumio",
  "data": {
    "mode": "storyArtist",
    "artist": "Pink Floyd"
  }
}
```

Example Respose:

```json
{
    "success": true,
    "data": {
        "type": "story",
        "value": "Pink Floyd were an English rock band formed in London in 1964..."
    }
}
```

#### Album Story

Retrieves the Album's Story and informations.

Payload:


```json
{
  "endpoint": "metavolumio",
  "data": {
    "mode": "storyAlbum",
    "artist": "Pink Floyd",
    "album": "The dark side of the moon"
  }
}
```

Example Respose:

```json
{
    "success": true,
    "data": {
        "type": "story",
        "value": "The Dark Side of the Moon is the eighth studio album by the English rock band Pink Floyd..."
    }
}
```

#### Album Credits

Retrieves the Album Credits (listing all known contributors and performers and their role)

Payload:


```json
{
  "endpoint": "metavolumio",
  "data": {
    "album": "Grace",
    "artist": "Jeff Buckley",
    "mode": "creditsAlbum"
  }
}
```

Example Respose:

```json
{
    "success": true,
    "data": {
        "type": "credits",
        "value": [
            {
                "key": "guitar",
                "values": [
                    {
                        "name": "Gary Lucas",
                        "uri": "mbid:/artist/d011c23d-e8e4-4b7b-90c8-63e26ee0bada"
                    },
                    {
                        "name": "Michael Tighe",
                        "uri": "mbid:/artist/5c5aed13-004e-4001-89af-269ddd847219"
                    }
                ]
            },
            {
                "key": "organ",
                "values": [
                    {
                        "name": "Loris Holland",
                        "uri": "mbid:/artist/9e7e54b0-0ad4-427c-9ca4-483e733e29ce"
                    }
                ]
            },
            {
                "key": "additional",
                "values": [
                    {
                        "name": "Clif Norrell",
                        "uri": "mbid:/artist/df8e1af4-c281-4d38-b06e-5f1f688c2111"
                    },
                    {
                        "name": "Jeff Buckley",
                        "uri": "mbid:/artist/e6e879c0-3d56-4f12-b3c5-3ce459661a8e"
                    }
                ]
            },
            {
                "key": "tabla",
                "values": [
                    {
                        "name": "Jeff Buckley",
                        "uri": "mbid:/artist/e6e879c0-3d56-4f12-b3c5-3ce459661a8e"
                    },
                    {
                        "name": "Misha Masud",
                        "uri": "mbid:/artist/ba56c279-f83a-4cd0-8395-9cf45483152e"
                    }
                ]
            },
            {
                "key": "vibraphone",
                "values": [
                    {
                        "name": "Matt Johnson",
                        "uri": "mbid:/artist/d39a5a70-de11-4ea3-a4c1-f2139cca265a"
                    }
                ]
            }
        ]
    }
}
```

Additionally, stories for artists, labels and places can be expanded. The mbid value is the mbid value (after last / in uri)

The values to use are:

storyPlace: if key === place

```json
{
  "endpoint": "metavolumio",
  "data": {
    "mbid": "d011c23d-e8e4-4b7b-90c8-63e26ee0bada",
    "mode": "storyPlace"
  }
}
```

storyLabel: if key === label

```json
{
  "endpoint": "metavolumio",
  "data": {
    "mbid": "cba24ea0-6965-4bfb-bc5b-4c303a11c16c",
    "mode": "storyLabel"
  }
}
```

storyArtist: everything else

```json
{
  "endpoint": "metavolumio",
  "data": {
    "mbid": "d011c23d-e8e4-4b7b-90c8-63e26ee0bada",
    "mode": "storyArtist"
  }
}
```
