# Study Buddy: a three-agent team in Telegram (Hermes Agent)

A Telegram group where a human asks to learn an ML topic and three agents cooperate by @mentioning each other.

## Agents
- Coordinator: only agent that talks to the human; runs the protocol (R1, R2...).
- Explainer: writes a short structured explanation. No tools.
- Quizzer: writes 3 quiz questions, grades answers, saves scores to a file (only agent with file access).

## Flow
Human -> Coordinator -> Explainer -> Coordinator -> Quizzer (QUIZ) -> Coordinator -> Human.
Answers: Human -> Coordinator -> Quizzer (GRADE) -> Coordinator -> Human.

## Setup
1. Install Hermes Agent and get an OpenRouter API key (You can install hermes on your machine); Do not forget to set spend limit to 0$ in openrouters API settings(It will force the API to use free models).
2. Create three bots with @BotFather in Telegram; disable privacy mode for each bot; turn on the bot-to-bot communication in bots settings.
3. Create three Hermes profiles (coordinator, explainer, quizzer) and setup a free model for every profile by ""hermes AGENT_NAME model setup"".
4. Copy each folder's SOUL.md and config.yaml into its profile.
5. Put keys in each profile's .env (not in this repo):
   OPENROUTER_API_KEY=... and TELEGRAM_BOT_TOKEN=...
6. In quizzer/SOUL.md replace [YOUR_PATH] with a writable absolute path.
7. Add all three bots to one Telegram group and start the gateway.
8. Send: "@study_buddy_coordinator_bot teach me gradient descent".

## Loop prevention
Bots reply only to specific tagged messages, once per task, and the final message has no @mention.

## Known limits
- Free model; strict formats can drift.
- Coordinator keeps the questions only in session context.
- Bot works if only your machine is on (to solve this I recommend deploy the Hermes in VPS server).
