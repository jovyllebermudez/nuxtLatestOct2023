<template>
  <div class="chatbot-container">
    <div class="chatbot-header">
      <h4>Ai assistant</h4>
      <button @click="$emit('close')">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          height="24px"
          viewBox="0 -960 960 960"
          width="24px"
          fill="#5f6368"
        >
          <path
            d="m256-200-56-56 224-224-224-224 56-56 224 224 224-224 56 56-224 224 224 224-56 56-224-224-224 224Z"
          />
        </svg>
      </button>
    </div>
    <div class="chatbot-body">
      <div v-for="message in messages" :key="message.id" class="chatbot-message">
        <p>{{ message.text }}</p>
      </div>
    </div>
    <div class="chatbot-footer">
      <input
        v-model="userInput"
        @keyup.enter="sendMessage"
        placeholder="Type a message..."
        class="p-3"
      />
      <button class="p-3" @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    skills: Array,
    projects: Array
  },
  data() {
    return {
      userInput: '',
      messages: []
    };
  },
  methods: {
    async sendMessage() {
      const userMessage = this.userInput;
      this.messages.push({ id: Date.now(), text: userMessage });
      this.userInput = '';

      const response = await fetch('/api/chatbot', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          message: userMessage,
          skills: this.skills,
          projects: this.projects
        })
      });

      const data = await response.json();
      const aiMessage = data.choices[0].message.content.trim();
      this.messages.push({ id: Date.now() + 1, text: aiMessage });
    }
  }
};
</script>

<style scoped>
.chatbot-container {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 310px;
  background: white;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
.chatbot-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 20px;
  border-bottom: 1px solid #ccc;
}
.chatbot-body {
  max-height: 400px;
  /* min-height: 400px; */
  overflow-y: auto;
  /* padding: 10px; */
}
.chatbot-footer {
  display: flex;
  padding: 10px;
  border-top: 1px solid #ccc;
}
.chatbot-message {
  margin-bottom: 10px;
  padding: 0px 10px;
}
</style>
