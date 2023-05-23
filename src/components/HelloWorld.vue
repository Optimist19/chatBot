<template>
  <div class="hello">
    <main>
      <section class="chatbot-container">
        <div class="chatbot-header">
          <img
            src="https://user-images.githubusercontent.com/14011726/94132137-7d4fc100-fe7c-11ea-8512-69f90cb65e48.gif"
            class="logo"
          />
          <h1>KnowItAll</h1>
          <h2>Ask me anything!</h2>
          <p class="supportId">User ID: 2344</p>
          <button class="clear-btn" id="clear-btn">start over</button>
        </div>
        <div class="chatbot-conversation-container" id="chatbot-conversation">
          <div class="speech speech-ai">How can I help you?</div>
        </div>
       
        <form id="form" class="chatbot-input-container">
          <input
            name="user-input"
            type="text"
            id="user-input"
            v-model="userInput"
            required
          />
          <button id="submit-btn" class="submit-btn" @click="btn">
            <img
              src="data:image/jpeg;base64,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"
              class="send-btn-icon"
            />
          </button>
        </form>
      </section>
    </main>
  </div>
</template>

<script>
import { Configuration, OpenAIApi } from "openai";
import { ref, onMounted } from "vue";

export default {
  name: "HelloWorld",
  setup() {
    let userInput = ref("");
    let chatbotConversation = ref(null);
    console.log(chatbotConversation);

    const configuration = new Configuration({
      apiKey: process.env.VUE_APP_OPENAI_API_KEY
    });
    const openai = new OpenAIApi(configuration);

    onMounted(() => {
      chatbotConversation.value = document.getElementById(
        "chatbot-conversation"
      );
    });

    const btn = (e) => {
      e.preventDefault();
      conversationArr.push({
        role: "user",
        content: userInput.value
      });
      const newSpeechBubble = document.createElement("div");
      newSpeechBubble.classList.add("speech-human", "speech");
      chatbotConversation.value.appendChild(newSpeechBubble);
      newSpeechBubble.innerText = userInput.value;
      userInput.value = "";
      chatbotConversation.value.scrollTop =
        chatbotConversation.value.scrollHeight;
      call();
    };

    let conversationArr = [
      {
        role: "system",
        content:
          "You are a highly knowledgeable assistant that is always happy to help."
      }
    ];

    async function call() {
      const response = await openai.createChatCompletion({
        model: "gpt-3.5-turbo",
        messages: conversationArr
      });

      console.log(response);

      
      renderTypewriterText(response.data.choices[0].message.content)
    }

    function renderTypewriterText(text) {
      const newSpeechBubble = document.createElement("div");
      newSpeechBubble.classList.add("speech", "speech-ai", "blinking-cursor");
      chatbotConversation.value.appendChild(newSpeechBubble);
      let i = 0;
      const interval = setInterval(() => {
        newSpeechBubble.textContent += text.slice(i - 1, i);
        if (text.length === i) {
          clearInterval(interval);
          newSpeechBubble.classList.remove("blinking-cursor");
        }
        i++;
        chatbotConversation.value.scrollTop = chatbotConversation.value.scrollHeight;
      }, 50);
    }

    return {
      btn,
      call,
      userInput,
      chatbotConversation
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
