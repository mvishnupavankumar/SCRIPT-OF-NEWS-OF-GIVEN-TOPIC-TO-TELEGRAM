# SCRIPT-OF-NEWS-OF-GIVEN-TOPIC-TO-TELEGRAM
News Script Generator to Telegram using n8n
📖 Description
This n8n workflow is a fantastic tool for content creators, marketers, or anyone who needs quick, engaging video scripts based on current news topics. It allows you to get a 60-second video script about any topic directly in your Telegram chat!

For Beginners: Just tell your Telegram bot what news topic you're interested in, and this workflow will find related news, then use AI to write a short video script for you, sending it right back to your chat.

For Tech Users: This workflow uses a Telegram Trigger to initiate the process. It then extracts your message using a Code node and sets it as the topic using a Set node. An HTTP Request node fetches news articles from the NewsData.io API based on the provided topic. Another Code node formats this news data. A subsequent HTTP Request node interacts with the OpenRouter AI API (specifically mistralai/mistral-7b-instruct) to generate a 60-second video script from the news. Finally, a Set node cleans the generated script, and a Telegram node sends the finished script back to your chat.

⚙️ How It Works (step-by-step with emojis)
🔹 1. Telegram Trigger 💬
Simple: This node listens for your messages in Telegram, starting the whole process when you send a news topic.

Tech: It's a Telegram Trigger node, configured to activate upon receiving a new message.

🔹 2. EXXTRACT DATA 📝
Simple: This node pulls the text of your Telegram message, which is your desired news topic.

Tech: A Code node extracts the text property from the incoming Telegram message object.

🔹 3. SEND TEXT ➡️
Simple: This node prepares your news topic for the next steps in the workflow.

Tech: A Set node assigns the extracted text from the previous node to a new variable called topic.

🔹 4. EXTRACT DATA FROM INTERNET 🌐
Simple: This node goes online to find relevant news articles based on the topic you provided.

Tech: An HTTP Request node makes a GET request to the NewsData.io API. It includes your YOUR_NEWSDATA_IO_API_KEY and sets the topic from the previous node as a header parameter to filter news by that topic in English from India.

🔹 5. SEND NEWS 📰
Simple: This node takes the raw news data and formats it into a readable list of titles and links.

Tech: A Code node processes the JSON response from the NewsData.io API. It maps each news result to a string containing its title and link, then joins them with double newlines. If no articles are found, it returns "No news articles found."

🔹 6. MAKE SCRIPT 🤖
Simple: This is where the magic happens! This node sends the news articles to an AI model to generate a video script.

Tech: An HTTP Request node sends a POST request to the OpenRouter AI chat completions API. It uses mistralai/mistral-7b-instruct as the model and crafts a prompt asking it to act as a video scriptwriter and create a 60-second script about the topic. It includes your YOUR_OPENROUTER_BEARER_TOKEN for authentication.

🔹 7. CLEAN SCRIPT AND SENDS 🧹
Simple: This node takes the AI-generated script and cleans it up, making it ready to be sent to you.

Tech: A Set node extracts the content of the AI's response (which is the generated script) and removes any newline characters, ensuring it's in a clean format for Telegram. This cleaned script is assigned to a variable named prompt.

🔹 8. SEND SCRIPT TO TELEGRAM 📤
Simple: The final step! This node sends the beautifully crafted video script directly to your Telegram chat.

Tech: A Telegram node, using your YOUR_TELEGRAM_CHAT_ID, sends the prompt (the cleaned script) as a message.

🔁 Replace the following before running:
🔐 REPLACE_ME for telegramApi credentials (e.g., " N8N TESTING")
Add your Telegram bot token to the Telegram credentials in n8n under the Credentials section and ensure it's linked to the Telegram nodes.

🌐 YOUR_NEWSDATA_IO_API_KEY
Replace this with your personal NewsData.io API key inside the "EXTRACT DATA FROM INTERNET" node's URL.

🪪 YOUR_OPENROUTER_BEARER_TOKEN
Replace this with your OpenRouter Bearer token in the Authorization header of the "MAKE SCRIPT" node.

💬 YOUR_TELEGRAM_CHAT_ID
Insert your personal Telegram chat ID in the "SEND SCRIPT TO TELEGRAM" node.

🧪 Testing Instructions
✅ Open n8n at http://localhost:5678 (or your n8n instance URL).
🔧 Click “Import Workflow” and paste the provided JSON content.
🔗 Ensure all connections between nodes are correctly established.
🔑 Navigate to the Credentials section in n8n and set up your Telegram API credential for your bot. Ensure the credential name matches "N8N TESTING".
🔄 In the "EXTRACT DATA FROM INTERNET" node, update the URL with your actual YOUR_NEWSDATA_IO_API_KEY.
🤖 In the "MAKE SCRIPT" node, update the Authorization header with your actual YOUR_OPENROUTER_BEARER_TOKEN.
💬 In the "SEND SCRIPT TO TELEGRAM" node, replace YOUR_TELEGRAM_CHAT_ID with your Telegram chat ID.
➡️ To test the workflow, activate it by toggling the "Active" switch.
📧 Send a message to your Telegram bot with the news topic you want a script for (e.g., "latest tech news", "environmental conservation efforts", "space exploration").
🧪 Click “Execute Node” on individual nodes to test each step independently and observe their outputs in the data flow.
🪵 Check the execution log at the bottom of the n8n interface to troubleshoot any issues or verify data flow.
📬 Check your Telegram chat for the generated 60-second video script!

💡 Tips for Beginners
💡 Always use the “Credentials” tab in n8n to store your API keys and tokens. This keeps your sensitive information secure and makes your workflows easily shareable without exposing credentials.
💡 After fetching data (like news articles), examine the output of the HTTP Request node. This helps you understand the data structure and how to extract the information you need.
💡 The Code node is very powerful for custom logic. Don't be afraid to experiment with it to transform data exactly as you need.
💡 If the AI-generated script isn't quite what you expected, try adjusting the prompt in the "MAKE SCRIPT" node to give the AI more specific instructions or examples.
💡 If your workflow isn't running as expected, check the "Execution" history in n8n for any error messages. They usually provide hints on what went wrong.












Canvas


