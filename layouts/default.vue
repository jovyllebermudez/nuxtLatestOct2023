<template>
  <div
    :class='" text-lg overflow-hidden flex flex-col tracking-wider " + (darkMode?"dark bg-ternary-dark":"bg-ternary-light ")'
  >
    <div class="container mx-auto px-4 max-w-6xl flex flex-col min-h-[100vh] text-primary-dark dark:text-primary-light">
      <section class="">
        <div class="container sm:mx-auto">
          <div
            class="py-6 md:py-12 flex items-center justify-between flex-col sm:flex-row"
          >
            <div
              class="font-bold flex text-xl sm:text-3xl my_hover px-2 justify-between w-full sm:w-auto"
            >
              <!-- <div class="sm:hidden">
                <DarkmodeBtn :toggleDarkMode="toggleDarkMode" />
              </div> -->
              <NuxtLink class="text-center" v-if="!isHomePage" to="/"> Home </NuxtLink>
              <div class="block sm:hidden text-right">
                <button
                  aria-label="show menu button"
                  @click="isMenuOpen = !isMenuOpen"
                  class="px-3 "
                >
                  <i v-if="isMenuOpen" class="bx bx-x my-1"></i>
                  <i v-if="!isMenuOpen" class="bx bx-menu my-1"></i>
                </button>
              </div>
            </div>
            <!-- <div
              :class="['font-bold sm:flex my-5 sm:my-0 space-x-0 sm:space-x-3 md:space-x-10  divide-y sm:justify-center divide-gray-200 sm:divide-y-0 w-[100vw] shadow-lg sm:shadow-none',isMenuOpen?'block':'hidden']"
            >
              <NuxtLink
                class="flex_center text-xl my_hover1 inline-flex py-3 sm:py-0 whitespace-nowrap"
                to="/about"
              >
                About
              </NuxtLink>
              <NuxtLink
                class="flex_center text-xl my_hover1 inline-flex py-3 sm:py-0"
                to="/projects"
              >
                Projects
              </NuxtLink>
              <NuxtLink
                class="flex_center text-xl my_hover1 inline-flex py-3 sm:py-0"
                to="/posts"
              >
                Posts
              </NuxtLink>
              <NuxtLink
                class="flex_center text-xl my_hover1 inline-flex py-3 sm:py-0"
                to="/uses"
              >
                Uses
              </NuxtLink>
              <NuxtLink
                class="flex_center text-xl my_hover1 inline-flex py-3 sm:py-0 sm:hidden"
                to="/contact"
              >
                Contact
              </NuxtLink>
            </div> -->
            <div class="hidden sm:flex sm:items-center text-base text-primary-light space-x-2">
              <!-- <div class="">
                <DarkmodeBtn :toggleDarkMode="toggleDarkMode" />
              </div> -->
              <!-- <NuxtLink class="" to="/contact">
                <button
                  id="contactbutton"
                  class=" scale-90 rounded-lg p-3 my_hover  bg-m4 px-4  "
                >
                  Contacts
                </button>
              </NuxtLink> -->
            </div>
          </div>
        </div>
      </section>
      <section class="flex-1">
        <slot />
      </section>
      <section class="footer-section w-[100%]">
        <div class="container mx-auto">
          <div
            class="pt-14 pb-10 flex-col sm:flex-row flex text-center justify-between"
          >
            <div class="my_hover">No Copyright © {{currentYear}}</div>
            <!-- <div class="my_hover">No Copyright © {{currentYear}} Jovylle</div> -->
            <div class="my_hover">
              <div class="">
                <DarkmodeBtn :toggleDarkMode="toggleDarkMode" />
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
    <button @click="toggleChatbot" class="chatbot-toggle-button">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        height="24px"
        viewBox="0 -960 960 960"
        width="24px"
        fill="#FFFFFF"
      >
        <path
          d="M240-400h320v-80H240v80Zm0-120h480v-80H240v80Zm0-120h480v-80H240v80ZM80-80v-720q0-33 23.5-56.5T160-880h640q33 0 56.5 23.5T880-800v480q0 33-23.5 56.5T800-240H240L80-80Zm126-240h594v-480H160v525l46-45Zm-46 0v-480 480Z"
        />
      </svg>
    </button>
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
      darkMode: false,
      currentYear: new Date().getFullYear(),
      isMenuOpen: false,
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
  computed: {
    isHomePage() {
      return this.$route.path === '/' || this.$route.path === '/home';
    }
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
    },
    toggleChatbot() {
      this.showChatbot = !this.showChatbot;
    }
  },
  mounted() {
    window.addEventListener('toggle-chatbot', this.toggleChatbot);
  },
  beforeDestroy() {
    window.removeEventListener('toggle-chatbot', this.toggleChatbot);
  }
}
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
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>