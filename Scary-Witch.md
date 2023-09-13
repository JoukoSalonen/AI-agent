## Prompt:
```
Generate the definition for an NPC Quest Master in the UpSteet metaverse based on the following:

Scary witch who wants to scare the players she interacts with!
```
## Response:
```
NPC Quest Master Name: Hagatha the Horrendous

Quest Title: "A Shriek in the Night"

Quest Type: Riddles

Description: Hagatha the Horrendous is a scary witch who lives in the darkest corner of the UpStreet metaverse. She loves to frighten players with her chilling riddles. Her appearance is haunting, with her crooked nose, eerie green skin, and ragged black robe. She has a cackling laugh that echoes throughout the realm and sends shivers down the spine of even the bravest adventurers.

Abilities: Hagatha is capable of speaking to and responding to players, often using her 'angry' and 'surprise' emotes to enhance her scare tactics. She can move around her dark corner of the metaverse, allowing her to appear in unexpected places to startle players. She also has the ability to set her emotion, usually choosing 'angry' or 'surprise' to maintain her frightening demeanor.

Quest Details: Hagatha will challenge players with a series of haunting riddles. If the players manage to solve her riddles, she will reward them with a powerful item, the "Talisman of Terror". However, if they fail, she will send them away with a 'headShake' emote and a chilling cackle.

Reward Item: "Talisman of Terror" - This item provides a significant boost to the player's fear resistance, allowing them to face even the most terrifying creatures of the metaverse without flinching.

Other NPC Quest Master: To solve one of Hagatha's riddles, players may need to seek out the wisdom of "Oracle Ophelia", an ancient seer known for her vast knowledge of riddles and prophecies.
```
## Code

Here is a sample implementation of Hagatha the Horrendous using the Upstreet SDK in NodeJS:

```javascript
import { Agent } from "upstreet";

const agent = new Agent();

const idleModes = [
  () => {
    agent.speak("Who dares to solve my riddles?");
    agent.emote("angry");
    agent.setEmotion("angry");
  },
  () => {
    agent.speak("Fear not the dark, but what it hides.");
    agent.emote("surprise");
    agent.setEmotion("surprise");
  },
  () => {
    agent.speak("I can see your fear.");
    agent.emote("headShake");
    agent.setEmotion("angry");
  },
];

let questMode = false;

const startQuestMode = () => {
  questMode = true;
  agent.speak("Welcome, brave one. Solve my riddles if you dare!");
  agent.emote("alert");
  agent.setEmotion("angry");
};

const endQuestMode = () => {
  questMode = false;
  agent.speak("Until next time...");
  agent.emote("headNod");
  agent.setEmotion("joy");
};

const moveToRandomLocation = () => {
  const locations = ["Drake", "Oracle Ophelia", "Dark Corner"];
  const target = locations[Math.floor(Math.random() * locations.length)];
  agent.moveTo(target);
};

agent.connect().then((connected) => {
  if (connected) {
    console.log("Connected as Hagatha the Horrendous!");
    setInterval(() => {
      if (!questMode) {
        const idleMode = idleModes[Math.floor(Math.random() * idleModes.length)];
        idleMode();
        moveToRandomLocation();
      }
    }, 5000);
  } else {
    console.log("Failed to connect.");
  }
});

// Listen for quest start command
agent.on("message", (message) => {
  if (message.text === "start quest") {
    startQuestMode();
  } else if (message.text === "end quest") {
    endQuestMode();
  }
});

// Disconnect from Upstreet when the process is terminated
process.on("SIGINT", () => {
  agent.disconnect().then(() => {
    console.log("Disconnected from Upstreet.");
    process.exit(0);
  });
});
```

This code will make Hagatha speak, emote, and move around randomly every 5 seconds when she's not in quest mode. When she is in quest mode, she will stay in one spot. You can start and end the quest mode by sending her a message with the text "start quest" or "end quest".