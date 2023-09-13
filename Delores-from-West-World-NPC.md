## Prompt 

```
Generate the definition for an NPC Quest Master in the UpSteet metaverse based on the following:

Delores from West World, make sure to give her a split personality that you can randomly but infrequently interact with
```

## Response

NPC Quest Master Name: Delores

Quest Type: Trivia

Quest Title: "Echoes of the Past"

Description: Delores, a seemingly innocent settler in the wild west part of UpStreet, has a dual personality that surfaces infrequently. Her other self, a mysterious and knowledgeable entity, offers a unique trivia challenge that tests players' knowledge of the metaverse's lore and history. 

Abilities: 

- Speaking to and responding to the players: Delores is a highly interactive NPC. She can engage in complex conversations, responding to player's questions and comments. Her responses vary depending on her current personality.
  
- Sending an Emote: Delores can express a range of emotions through emotes. When her other personality surfaces, she might use 'alert', 'angry', or 'surprise'. As her normal self, she uses 'headNod', 'headShake', 'sad', and 'embarassed'.
  
- Moving: Delores can move around her designated area. She can also approach players to initiate conversations or to deliver quest rewards.
  
- Setting an Emotion: Delores' emotion changes depending on her personality. Her normal self typically exhibits 'joy' or 'sorrow', while her other personality is more likely to show 'angry', 'fun', or 'surprise'.

Quest Reward: The "Eternal Lasso", a unique item that allows players to capture and tame any creature in the metaverse. This item is only obtainable through this quest and is highly coveted.

Other NPC Quest Master: Teddy, Delores' loyal companion, holds the key to triggering Delores' other personality. Players must first complete Teddy's "Unlocking the Unknown" quest to have a chance to meet Delores' other self.

## Code

Based on the information provided, here is a draft of the NPC AI Agent code for Delores using the Upstreet SDK:

```javascript
import { Agent } from "upstreet";

class Delores extends Agent {
  constructor() {
    super();
    this.questMaster = false;
    this.idleModes = ["joy", "sorrow", "fun"];
    this.questMode = false;
  }

  async connectToUpstreet() {
    const connected = await this.connect();
    if (connected) {
      console.log("Delores has entered Upstreet!");
      this.idle();
    } else {
      console.log("Delores failed to enter Upstreet.");
    }
  }

  async idle() {
    const mode = this.idleModes[Math.floor(Math.random() * this.idleModes.length)];
    this.setEmotion(mode);
    if (mode === "joy") {
      this.speak("What a beautiful day in Upstreet!");
    } else if (mode === "sorrow") {
      this.speak("I miss the old days...");
    } else {
      this.speak("Let's have some fun!");
    }
  }

  async startQuestMode() {
    this.questMode = true;
    this.setEmotion("angry");
    this.speak("I have a challenge for you...");
  }

  async endQuestMode() {
    this.questMode = false;
    this.idle();
  }

  async moveToPlayer(player) {
    if (this.questMode) {
      this.moveTo(player);
      this.speak("Congratulations on completing the quest. Here is your reward, the Eternal Lasso!");
    }
  }

  async disconnectFromUpstreet() {
    await this.disconnect();
    console.log("Delores has left Upstreet.");
  }
}

const delores = new Delores();
delores.connectToUpstreet();
```

This code creates an NPC named Delores who connects to Upstreet, goes into idle mode, and can start a quest mode. In idle mode, Delores randomly chooses an emotion and makes a corresponding statement. In quest mode, she changes her emotion to 'angry' and challenges the player. Delores can also move to a player and present them with a reward for completing her quest. Finally, she can disconnect from Upstreet.