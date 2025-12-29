<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const TELEGRAM_REGEX = /^[a-zA-Z][a-zA-Z0-9_]{4,31}$/;
const MIN_NAME_LENGTH = 2;
const MAX_NAME_LENGTH = 50;
const MIN_MESSAGE_LENGTH = 10;
const MAX_MESSAGE_LENGTH = 1000;

const Icons = {
  SocialMedia: [
    {
      name: "Linkedin",
      url: "M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z",
      viewBox: "0 0 24 24",
    },
    {
      name: "Facebook",
      url: "M512 256C512 114.6 397.4 0 256 0S0 114.6 0 256C0 376 82.7 476.8 194.2 504.5V334.2H141.4V256h52.8V222.3c0-87.1 39.4-127.5 125-127.5c16.2 0 44.2 3.2 55.7 6.4V172c-6-.6-16.5-1-29.6-1c-42 0-58.2 15.9-58.2 57.2V256h83.6l-14.4 78.2H287V510.1C413.8 494.8 512 386.9 512 256h0z",
      viewBox: "0 0 512 512",
    },
    {
      name: "GitHub",
      url: "M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.835 2.809 1.305 3.493.998.108-.776.417-1.305.76-1.605-2.665-.304-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.046.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z",
      viewBox: "0 0 24 24",
    },
  ],
};

const getSocialLink = (name) => {
  const links = {
    Linkedin: "https://www.linkedin.com/in/yourlinkedinprofile/",
    Facebook: "https://web.facebook.com/PichsovandaraDevit",
    GitHub: "https://github.com/IsMeVit",
  };
  return links[name] || "#";
};

const showContactForm = ref(false);
const isMobile = ref(false);
const name = ref("");
const telegram = ref("");
const message = ref("");
const isSent = ref(false);
const honeypot = ref("");
const errors = ref({ name: "", telegram: "", message: "" });
let messageTimeout = null;

const validateForm = () => {
  let isValid = true;
  errors.value = { name: "", telegram: "", message: "" };

  if (
    name.value.length < MIN_NAME_LENGTH ||
    name.value.length > MAX_NAME_LENGTH
  ) {
    errors.value.name = `Name must be between ${MIN_NAME_LENGTH} and ${MAX_NAME_LENGTH} characters.`;
    isValid = false;
  }

  if (!telegram.value.length || !TELEGRAM_REGEX.test(telegram.value)) {
    errors.value.telegram = "Invalid Telegram username (5-32 chars, no @).";
    isValid = false;
  }

  if (
    message.value.length < MIN_MESSAGE_LENGTH ||
    message.value.length > MAX_MESSAGE_LENGTH
  ) {
    errors.value.message = `Message must be between ${MIN_MESSAGE_LENGTH} and ${MAX_MESSAGE_LENGTH} characters.`;
    isValid = false;
  }
  return isValid;
};

const showForm = () => (showContactForm.value = true);
const showIcon = () => (showContactForm.value = false);

const handleResize = () => {
  const width = window.innerWidth;
  if (width >= 768) {
    isMobile.value = false;
    showContactForm.value = true;
  } else {
    isMobile.value = true;
  }
};

const sendToTelegram = async () => {
  if (!validateForm()) return;

  const webhookUrl = "/api/webhook";

  if (messageTimeout) {
    clearTimeout(messageTimeout);
    messageTimeout = null;
  }

  try {
    const res = await fetch(webhookUrl, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        name: name.value,
        telegram: telegram.value,
        message: message.value,
        honeypot: honeypot.value,
      }),
    });

    if (res.ok) {
      isSent.value = true;
      name.value = telegram.value = message.value = honeypot.value = "";
      if (isMobile.value) showIcon();
      messageTimeout = setTimeout(() => (isSent.value = false), 5000);
    } else {
      const errorData = await res.json().catch(() => ({}));
      alert(`Submission Failed: ${errorData.message || res.statusText}`);
    }
  } catch (error) {
    alert("Failed to send message. Please try again.");
  }
};

onMounted(() => {
  handleResize();
  window.addEventListener("resize", handleResize);
});

onUnmounted(() => window.removeEventListener("resize", handleResize));
</script>

<template>
  <div
    data-aos="fade-enter-active"
    data-aos-delay="200"
    class="min-h-screen flex flex-col items-center justify-center p-4 md:p-10 relative z-10 font-sans"
  >
    <header class="text-center mb-12 max-w-2xl">
      <h1
        class="text-4xl md:text-6xl font-black text-white tracking-tighter mb-4"
      >
        Let’s
        <span
          class="animate-gradient-text bg-linear-to-r from-purple-400 via-cyan-300 to-blue-400 bg-clip-text text-transparent bg-size-[200%_auto]"
          >Connect</span
        >
      </h1>
      <p class="text-gray-400 text-lg">
        Got a project or just want to chat? I'm just a message away.
      </p>
    </header>

    <div class="max-w-5xl w-full grid grid-cols-1 md:grid-cols-12 gap-6">
      <section class="md:col-span-4">
        <div
          class="bg-white/10 backdrop-blur-xl border border-white/20 rounded-[2.5rem] p-8 shadow-2xl flex flex-col justify-start items-center h-full"
        >
          <h2
            class="text-indigo-300 font-mono text-xs uppercase tracking-[0.3em] text-center opacity-70 group-hover/card:opacity-100 transition-opacity"
          >
            Find Me Online
          </h2>
          <div class="mb-10 h-px w-60 bg-linear-to-r from-transparent via-indigo-500 to-transparent opacity-50 shadow-[0_0_8px_rgba(99,102,241,0.8)]"></div>
          
          <div class="grid grid-cols-3 md:grid-cols-1 gap-6">
            <a
              v-for="icon in Icons.SocialMedia"
              :key="icon.name"
              :href="getSocialLink(icon.name)"
              target="_blank"
              class="flex items-center md:justify-start justify-center gap-4 group transition-all"
            >
              <div
                class="p-3 bg-white/5 rounded-2xl border border-white/10 group-hover:border-purple-500/50 group-hover:bg-purple-500/10 group-hover:shadow-[0_0_15px_rgba(168,85,247,0.4)] transition-all"
              >
                <svg
                  width="24"
                  height="24"
                  :viewBox="icon.viewBox"
                  fill="currentColor"
                  class="text-white group-hover:text-purple-400"
                >
                  <path :d="icon.url"></path>
                </svg>
              </div>
              <span
                class="hidden md:block text-gray-300 font-bold group-hover:text-white transition-colors"
                >{{ icon.name }}</span
              >
            </a>
          </div>
        </div>
      </section>

      <section
        class="md:col-span-8 bg-black/30 backdrop-blur-xl border border-white/10 rounded-[2.5rem] p-8 md:p-10 shadow-2xl relative overflow-hidden"
      >
        <div
          v-if="isMobile && !showContactForm"
          @click="showForm"
          class="flex flex-col items-center justify-center py-10 cursor-pointer group"
        >
          <div
            class="w-20 h-20 bg-purple-600/20 rounded-full flex items-center justify-center mb-4 border border-purple-500/30 group-hover:scale-110 transition-transform shadow-[0_0_20px_rgba(168,85,247,0.2)]"
          >
            <span class="text-3xl">🚀</span>
          </div>
          <span class="text-xl font-bold text-white">Send a Message</span>
          <p class="text-sm text-gray-500 mt-2">Tap to open form</p>
        </div>

        <div
          v-if="showContactForm || !isMobile"
          :class="{ block: true, hidden: isMobile && !showContactForm }"
        >
          <div class="flex justify-between items-center mb-8">
            <h2 class="text-2xl font-black text-white tracking-tight">
              Send a Message
            </h2>
            <button
              v-if="isMobile"
              @click="showIcon"
              class="text-gray-500 hover:text-white text-xs font-mono uppercase tracking-widest"
            >
              Close &times;
            </button>
          </div>

          <form @submit.prevent="sendToTelegram" class="space-y-5">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
              <div>
                <label
                  class="block text-[10px] uppercase tracking-widest text-gray-500 font-bold mb-2 ml-1"
                  >Your Name</label
                >
                <input
                  v-model="name"
                  type="text"
                  placeholder="John Doe"
                  :class="[
                    'w-full px-4 py-4 bg-white/5 border rounded-2xl focus:ring-2 focus:ring-purple-500 outline-none transition-all text-white',
                    errors.name ? 'border-red-500/50' : 'border-white/10',
                  ]"
                />
                <p
                  v-if="errors.name"
                  class="text-red-400 text-[10px] mt-1 ml-1 uppercase"
                >
                  {{ errors.name }}
                </p>
              </div>
              <div>
                <label
                  class="block text-[10px] uppercase tracking-widest text-gray-500 font-bold mb-2 ml-1"
                  >Telegram User</label
                >
                <input
                  v-model="telegram"
                  type="text"
                  placeholder="username_only"
                  :class="[
                    'w-full px-4 py-4 bg-white/5 border rounded-2xl focus:ring-2 focus:ring-purple-500 outline-none transition-all text-white',
                    errors.telegram ? 'border-red-500/50' : 'border-white/10',
                  ]"
                />
                <p
                  v-if="errors.telegram"
                  class="text-red-400 text-[10px] mt-1 ml-1 uppercase"
                >
                  {{ errors.telegram }}
                </p>
              </div>
            </div>

            <div>
              <label
                class="block text-[10px] uppercase tracking-widest text-gray-500 font-bold mb-2 ml-1"
                >Message</label
              >
              <textarea
                v-model="message"
                rows="4"
                placeholder="How can I help you?"
                :class="[
                  'w-full px-4 py-4 bg-white/5 border rounded-2xl focus:ring-2 focus:ring-purple-500 outline-none transition-all text-white resize-none',
                  errors.message ? 'border-red-500/50' : 'border-white/10',
                ]"
              ></textarea>
              <p
                v-if="errors.message"
                class="text-red-400 text-[10px] mt-1 ml-1 uppercase"
              >
                {{ errors.message }}
              </p>
            </div>

            <input type="text" v-model="honeypot" style="display: none" />

            <button
              type="submit"
              class="w-full py-4 bg-white text-black rounded-2xl font-black text-sm uppercase tracking-widest hover:bg-purple-500 hover:text-white hover:shadow-[0_0_20px_rgba(168,85,247,0.5)] transition-all active:scale-95 flex items-center justify-center gap-2"
            >
              Send Message 🚀
            </button>

            <transition name="fade">
              <p
                v-if="isSent"
                class="text-green-400 text-center font-bold text-sm animate-bounce"
              >
                ✅ Message sent to Telegram!
              </p>
            </transition>
          </form>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
@keyframes gradient-text {
  0%,
  100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}
.animate-gradient-text {
  animation: gradient-text 4s ease infinite;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
