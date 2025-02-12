<template>
  <div>
    <NuxtPage />
    <button @click="toggleChatbot" class="chatbot-toggle-button">Chat with me</button>
    <Chatbot v-if="showChatbot" :skills="skills" :projects="projects" @close="toggleChatbot" />
  </div>
</template>

<script>
import Chatbot from '~/components/Chatbot.vue';

export default {
  components: {
    Chatbot
  },
  data() {
    return {
      showChatbot: false,
      skills: ["JavaScript", "Nuxt.js", "Vue.js", "CSS", "HTML"], // Example skills
      projects: [
        {
          name: "Portfolio Website",
          description: "A personal portfolio website to showcase my projects and skills.",
          link: "https://example.com"
        },
        {
          name: "Chatbot Integration",
          description: "A chatbot integrated into a website using OpenAI's GPT model.",
          link: "https://example.com"
        }
      ] // Example projects
    };
  },
  methods: {
    toggleChatbot() {
      this.showChatbot = !this.showChatbot;
    }
  }
};
</script>

<style scoped>
.chatbot-toggle-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  font-size: 24px;
  cursor: pointer;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
</style>