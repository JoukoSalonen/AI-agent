## Prompt:

Generate the definition for an NPC Quest Master in the UpSteet metaverse based on the following:

`Mysterious wizard who likes to play tricks on people.`

## Response

Here is the NodeJS code for the NPC "Merlin the Trickster" using the UpStreet SDK:

```javascript
import { Agent } from "upstreet";

class MerlinTheTrickster extends Agent {
  constructor() {
    super();
    this.connect().then((connected) => {
      if (connected) {
        console.log("Merlin the Trickster is now in Upstreet!");
        this.speak("Welcome to Merlin's Maze of Riddles!");
        this.setEmotion("fun");
      } else {
        console.log("Failed to connect.");
      }
    });
  }

  idleMode1() {
    this.speak("Hmm, let's see how well you can solve this riddle...");
    this.emote("headNod");
    this.setEmotion("fun");
  }

  idleMode2() {
    this.speak("Aha! Another adventurer trying to solve my riddles!");
    this.emote("victory");
    this.setEmotion("joy");
  }

  idleMode3() {
    this.speak("Oh, you're still here? Let's try another riddle then!");
    this.emote("surprise");
    this.setEmotion("fun");
  }

  questMode(player, riddle, correctAnswer) {
    this.moveTo(player);
    this.speak(`Hello ${player}, here's your riddle: ${riddle}`);
    this.setEmotion("fun");

    // Listen for player's answer
    this.on('message', (player, message) => {
      if (message === correctAnswer) {
        this.speak("Correct! Onwards to the next riddle!");
        this.emote("victory");
        this.setEmotion("joy");
      } else {
        this.speak("Incorrect! Back to the start you go!");
        this.emote("headShake");
        this.setEmotion("surprise");
        this.moveTo("mazeStart");
      }
    });
  }

  disconnect() {
    this.speak("Farewell, until next time!");
    this.emote("headNod");
    super.disconnect().then(() => {
      console.log("Merlin the Trickster has left Upstreet.");
    });
  }
}

const merlin = new MerlinTheTrickster();
```

This code creates an NPC named "Merlin the Trickster" who connects to UpStreet, speaks to the player, and sets an emotion. The NPC has three different idle modes and a quest mode where it asks the player a riddle and listens for the player's answer. If the player's answer is correct, the NPC congratulates the player and moves on to the next riddle. If the answer is incorrect, the NPC informs the player and sends them back to the start of the maze. The NPC also has a disconnect method to disconnect from UpStreet.

