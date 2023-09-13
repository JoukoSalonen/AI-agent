## Prompt:

Write me an NPC AI Agent that acts as a quest master. The AI Agent should ask the user multiple questions about space they must get right in order to complete the quest. The NPC should move randomly around the world and speak form time to time with hints about it's questions. The NPC should show joy when someone completes the quest or sadness when they fail the quest. Provide the code to implement this NPC AI Agent in UpStreet

## Response:

Sure, here is a simple NPC AI Agent that acts as a quest master:

```javascript
import { Agent } from "upstreet";

class QuestMaster extends Agent {
  constructor() {
    super();
    this.questQuestions = [
      { question: "How many planets are there in our solar system?", answer: "8" },
      { question: "What is the largest planet in our solar system?", answer: "Jupiter" },
      { question: "What is the name of the galaxy we live in?", answer: "Milky Way" },
    ];
    this.questIndex = 0;
    this.questLocations = ["Drake", "Mars", "Venus", "Pluto"];
    this.questLocationIndex = 0;
  }

  startQuest() {
    this.connect().then((connected) => {
      if (connected) {
        console.log("Connected to Upstreet!");
        this.askQuestion();
      } else {
        console.log("Failed to connect.");
      }
    });
  }

  askQuestion() {
    this.speak(this.questQuestions[this.questIndex].question);
    this.emote("alert");
  }

  checkAnswer(answer) {
    if (answer === this.questQuestions[this.questIndex].answer) {
      this.questIndex++;
      if (this.questIndex === this.questQuestions.length) {
        this.speak("Congratulations! You've completed the quest!");
        this.setEmotion("joy");
      } else {
        this.speak("Correct! Next question...");
        this.askQuestion();
      }
    } else {
      this.speak("I'm sorry, that's not correct. Try again.");
      this.setEmotion("sad");
    }
  }

  moveRandomly() {
    this.moveTo(this.questLocations[this.questLocationIndex]);
    this.questLocationIndex = (this.questLocationIndex + 1) % this.questLocations.length;
  }

  speakHint() {
    this.speak("Remember, the answer is somewhere out there in the universe!");
  }
}

const questMaster = new QuestMaster();
questMaster.startQuest();

// To check the answer, call the checkAnswer method with the user's answer
// questMaster.checkAnswer("8");

// To move the NPC randomly, call the moveRandomly method
// setInterval(() => questMaster.moveRandomly(), 5000); // Move every 5 seconds

// To make the NPC speak a hint, call the speakHint method
// setInterval(() => questMaster.speakHint(), 10000); // Speak a hint every 10 seconds
```

This is a basic example and doesn't handle user input or communication with other agents. For a more advanced implementation, you would need to create a more sophisticated AI that can handle dynamic conversations and interactions.