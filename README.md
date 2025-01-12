# Voice support tools and scripts for Music Assistant

Bridge the gap between Home Assistant Assist and Music Assistant for voice-initiated music control.

This repository is meant to be an effort to collect scripts, blueprints, HOWto's etc. and their translations to enable full Voice control of music playback.
Home Assistant itself has very limited intents for music/media control, and especially there is no support for initiating playback of music by voice.
While this support is on the horizon to be added, there is still a lot to investigate about that to create a universal way to provide that support in HA natively. Maybe the resources/experiments from this repository can help make that journey easier in the future.

**Community driven effort!**
Please reach out if you want to help out or have great ideas!
If you have something to share here, feel free to PR it or ask to be added to the maintainers.

## Option 1: Local Assistant Blueprint

Blueprint to initiate media playback using pure local intent handling (custom sentences) so no Cloud-LLM involved.
This however means that requests need to be very carefuly formulated.

The Blueprint is located in the local-assistant-blueprint folder of this repository.

### Usage

All sentences must:

- start with the words `Play` or `Listen to` followed by the item type `artist/track/album/playlist/radio station` and then the name of the item

- for album and track be optionally followed by `by (the) artist` and then the artist name

- then be optionally followed by an area name or device name

- then, for artist, track, album or playlist, be optionally followed by the phrase `using radio mode`

#### Acceptable variations

There are acceptable variations to some words and inclusion of the word `the` is optional.

#### Examples

```

Play the artist Pink Floyd in the kitchen

Listen to album Jagged Little Pill in the study

Listen to the album Greatest Hits by the artist James Taylor in the kitchen

Play track New Years Day in the bedroom

Play track New Years Day in the bedroom using radio mode

Play the song A Hard Days Night by Billy Joel in the bedroom

Listen to the playlist Classic Rock in the study

Listen to the radio station BBC Radio 1 in the bedroom

Play the album Classical Nights on the Bedroom Sonos Speaker

Listen to the record Classical Nights on the Bedroom Sonos Speaker

Play the band U2
```

## Option 2

Script which can be used by an LLM integration like [Open AI Conversation](https://www.home-assistant.io/integrations/openai_conversation/) (ChatGPT) or [Google Generative AI](https://www.home-assistant.io/integrations/google_generative_ai_conversation/) (Gemini).

The script is located in the `llm_script` folder of this repository.

The language of the voice command is not relevant, the script has all descriptions in English, but it will be used by voice commands issued in a different language as well.

### Prerequisites

1. An LLM integration needs to be set up, and used in your Voice pipeline
2. The script needs to be added to your configuration
3. The script must be exposed to Assist

### Usage

There is no required format for the sentences, just use anything you can imagine to play music. You can add an area in which it should be played. If the area is ommited from your voice request, it will take the area from which the command is issued.

It will differ per LLM integration how well the commands are understood. If the command is not clear enough, the LLM might ask for more details.

### Examples
All responses and results are generated each time the script is used, so don't expect the exact same results as below.

- Command: *Play that the album from that grunge band with the baby swimmng towards a bank note on the album cover in the room in which we prepare our meals*
  
  Response:  *The album "Nevermind" by Nirvana is now playing in the area in which meals are prepared*
  
  Result: The album "Nevermind" will be played in the kitchen

- Command: *Play some classic rock songs*
  
  Response: *I've started playing some classic rock songs in the office. Enjoy the music!*

  Result: The following 5 songs are played
    * Led Zeppelin - Stairway to Heaven
    * Queen - Bohemian Rhapsody
    * The Rolling Stones - Paint It Black
    * The Who - My Generation
    * AC/DC - Back in Black