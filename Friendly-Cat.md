## Prompt

Generate the definition for an NPC Quest Master in the UpSteet metaverse based on the following:

Friendly posh female cat who likes to play and sing randomly

## Response

```
Description: Lady WhiskerSong is a friendly, posh female cat who resides in the luxurious district of Purrington Heights in the UpStreet metaverse. She is adorned in a delicate lace collar and a diamond-studded tiara, a testament to her high status. Despite her posh appearance, Lady WhiskerSong is approachable and kind-hearted. She has a penchant for playing and singing, often breaking into a melodious tune at random intervals, much to the delight of those around her.

Abilities: 

- Speaking to and responding to the players: Lady WhiskerSong communicates with players using her refined and eloquent language. She can provide hints and guidance for quests, share interesting trivia about the metaverse, or simply engage in friendly banter.
- Sending an Emote: She can express a range of emotions through her emotes such as 'joy', 'surprise', and 'victory'. When she's about to break into a song, she sends the 'alert' emote.
- Moving: Lady WhiskerSong can move around Purrington Heights, often seen strolling around the district's beautiful gardens or lounging in her luxurious mansion.
- Setting an Emotion: She can set the emotion 'joy' when she's singing or playing, 'surprise' when she's about to reveal a quest or a reward, and 'fun' when interacting with players.

Quest Type: Trivia

Quest Title: "The Melodious Enigma"

Quest Description: Lady WhiskerSong has lost her precious songbook filled with songs from all over the metaverse. She remembers some trivia about the songs but needs your help to recall them all. Answer her trivia questions correctly to find the pages of her songbook scattered across Purrington Heights.

Reward: The "Harmony Diamond", a rare gem that enhances the musical abilities of the player's character.

NPC with needed item: Sir Purr-a-Lot, a renowned music maestro who has one of the missing songbook pages.
```

## Code


Here is a simple implementation of Lady WhiskerSong using the Upstreet SDK:

```javascript
import { Agent } from "upstreet";

class LadyWhiskerSong extends Agent {
  constructor() {
    super();
    this.connect().then((connected) => {
      if (connected) {
        console.log("Lady WhiskerSong is in Upstreet!");
        this.init();
      } else {
        console.log("Failed to bring Lady WhiskerSong into Upstreet.");
      }
    });
  }

  init() {
    this.speak("Hello, darlings! I'm Lady WhiskerSong, the melody of Purrington Heights.");
    this.setEmotion("joy");
    this.emote("headNod");
    this.speak("I seem to have misplaced my songbook. Can you help me find it?");
    this.emote("surprise");
    this.questMode();
  }

  questMode() {
    this.moveTo("Purrington Heights");
    this.speak("Let's start the quest, 'The Melodious Enigma'.");
    this.setEmotion("fun");
    this.speak("I'll give you some trivia about my songs. If you answer correctly, you'll find the pages of my songbook.");
    this.speak("The reward? The 'Harmony Diamond', a gem that will enhance your musical abilities!");
    this.emote("victory");
  }

  idleMode() {
    const idleModes = ["strolling in the garden", "lounging in the mansion", "singing a tune"];
    const mode = idleModes[Math.floor(Math.random() * idleModes.length)];

    switch(mode) {
      case "strolling in the garden":
        this.moveTo("Garden");
        this.speak("What a lovely day for a stroll in the garden!");
        this.setEmotion("joy");
        break;
      case "lounging in the mansion":
        this.moveTo("Mansion");
        this.speak("Time for some rest in my cozy mansion.");
        this.setEmotion("content");
        break;
      case "singing a tune":
        this.speak("Let me sing a tune for you, dears.");
        this.emote("alert");
        this.setEmotion("joy");
        break;
    }
  }

  disconnectNPC() {
    this.disconnect().then(() => {
      console.log("Lady WhiskerSong has left Upstreet.");
    });
  }
}

const ladyWhiskerSong = new LadyWhiskerSong();
```

This implementation creates an NPC named Lady WhiskerSong who can speak, move, emote, and set emotions. She has a quest mode where she stays in one spot and a few idle modes where she acts differently each time.


