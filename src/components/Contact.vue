<script setup>
import { ref, reactive, onMounted, onBeforeUnmount } from "vue";

// ======================================
// CONFIGURATION
// ======================================
const ACCESS_KEY = import.meta.env.VITE_WEB3FORMS_ACCESS_KEY || "";

const API_URL = "https://api.web3forms.com/submit";

// ======================================
// ANIMATION
// ======================================
const contactSection = ref(null);
const isVisible = ref(false);
let observer = null;

onMounted(() => {
  if (typeof IntersectionObserver === "undefined") {
    isVisible.value = true;
    return;
  }

  observer = new IntersectionObserver(
    (entries) => {
      if (entries[0]?.isIntersecting) {
        isVisible.value = true;
        observer?.disconnect();
      }
    },
    { threshold: 0.1 },
  );

  if (contactSection.value) {
    observer.observe(contactSection.value);
  }
});

onBeforeUnmount(() => {
  observer?.disconnect();
});

// ======================================
// CONTACT DETAILS
// ======================================
const contactInfo = [
  {
    label: "Email",
    value: "kakveyket408@gmail.com",
    href: "mailto:kakveyket408@gmail.com",
  },
  {
    label: "Phone",
    value: "+855 96 763 7609",
    href: "tel:+855967637609",
  },
  {
    label: "Telegram",
    value: "@VKak_vey",
    href: "https://t.me/VKak_vey",
  },
];

const socials = [
  {
    name: "GitHub",
    href: "https://github.com/KakveyKet",
  },
  {
    name: "LinkedIn",
    href: "https://www.linkedin.com/in/kakvey-ket-b22203364",
  },
  {
    name: "Facebook",
    href: "https://www.facebook.com/profile.php?id=61584525802922",
  },
  {
    name: "YouTube",
    href: "https://www.youtube.com/@KakveyKet",
  },
];

// ======================================
// FORM STATE
// ======================================
const form = reactive({
  name: "",
  email: "",
  subject: "",
  message: "",
  botcheck: false,
});

const isSending = ref(false);
const status = ref("");
const statusMessage = ref("");

// ======================================
// SUBMIT HANDLER
// ======================================
async function sendMessage() {
  if (isSending.value) return;

  status.value = "";
  statusMessage.value = "";

  if (!ACCESS_KEY) {
    status.value = "error";
    statusMessage.value =
      "Contact form is not configured. Please use email or Telegram.";
    return;
  }

  isSending.value = true;

  try {
    const payload = {
      access_key: ACCESS_KEY,
      name: form.name.trim(),
      email: form.email.trim(),
      subject: form.subject.trim(),
      message: form.message.trim(),
      botcheck: form.botcheck,
    };

    const response = await fetch(API_URL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
      body: JSON.stringify(payload),
    });

    const result = await response.json().catch(() => null);

    if (!response.ok || result?.success !== true) {
      throw new Error(
        result?.message || `Unable to submit message (${response.status}).`,
      );
    }

    status.value = "success";
    statusMessage.value =
      "Your message was sent successfully! Thank you for contacting me.";

    // Reset only after a successful response.
    form.name = "";
    form.email = "";
    form.subject = "";
    form.message = "";
    form.botcheck = false;
  } catch (error) {
    console.error("Email submission failed:", error);

    status.value = "error";
    statusMessage.value =
      error instanceof Error
        ? error.message
        : "Unable to send your message. Please try again.";
  } finally {
    isSending.value = false;
  }
}

// ======================================
// INPUT STYLES
// ======================================
const inputClass = `
  peer w-full border-b-2 border-zinc-200
  bg-transparent py-2.5 text-lg font-medium
  text-zinc-900 placeholder-transparent
  outline-none transition-colors duration-300
  focus:border-blue-600
  dark:border-zinc-700 dark:text-white
  dark:focus:border-blue-500
`;

const labelClass = `
  absolute left-0 -top-4 cursor-text
  text-xs font-bold uppercase tracking-wider
  text-zinc-400 transition-all duration-300
  peer-placeholder-shown:top-2.5
  peer-placeholder-shown:text-base
  peer-placeholder-shown:font-normal
  peer-focus:-top-4 peer-focus:text-xs
  peer-focus:font-bold peer-focus:text-blue-600
  dark:peer-focus:text-blue-400
`;
</script>

<template>
  <section
    id="contact"
    ref="contactSection"
    class="scroll-mt-24 pb-10 sm:scroll-mt-32 sm:pb-20"
  >
    <div
      class="flex flex-col overflow-hidden rounded-[2rem] bg-zinc-900 text-white shadow-2xl dark:border dark:border-zinc-800 dark:bg-zinc-950 dark:shadow-none sm:rounded-[2.5rem] lg:flex-row"
      :class="isVisible ? 'animate-slide-up' : 'opacity-0'"
    >
      <!-- LEFT: CONTACT INFORMATION -->
      <div
        class="relative flex flex-col justify-between overflow-hidden border-b border-zinc-800 p-8 sm:p-12 lg:w-2/5 lg:border-b-0 lg:border-r lg:p-16"
      >
        <div
          class="pointer-events-none absolute -bottom-32 -left-32 h-64 w-64 rounded-full bg-blue-600 opacity-30 blur-[100px]"
        ></div>

        <div class="relative z-10">
          <h2
            class="mb-4 text-3xl font-bold tracking-tight text-white sm:text-4xl"
          >
            Let's build something.
          </h2>

          <p
            class="mb-10 max-w-sm text-base font-light leading-relaxed text-zinc-400 sm:mb-12 sm:text-lg"
          >
            Have a project in mind? Reach out and let's discuss how I can help
            your business grow.
          </p>

          <div class="space-y-8">
            <div v-for="info in contactInfo" :key="info.label" class="group">
              <p
                class="mb-1 text-xs font-semibold uppercase tracking-widest text-zinc-500"
              >
                {{ info.label }}
              </p>

              <a
                :href="info.href"
                :target="info.label === 'Telegram' ? '_blank' : undefined"
                :rel="
                  info.label === 'Telegram' ? 'noopener noreferrer' : undefined
                "
                class="relative inline-flex max-w-full overflow-hidden text-lg font-medium text-zinc-100 sm:text-xl"
              >
                <span
                  class="block break-all transition-transform duration-300 group-hover:-translate-y-full"
                >
                  {{ info.value }}
                </span>

                <span
                  aria-hidden="true"
                  class="absolute inset-0 block translate-y-full break-all text-blue-400 transition-transform duration-300 group-hover:translate-y-0"
                >
                  {{ info.value }}
                </span>
              </a>
            </div>
          </div>
        </div>

        <!-- SOCIAL LINKS -->
        <div class="relative z-10 mt-16 flex flex-wrap gap-4 sm:mt-20 sm:gap-6">
          <a
            v-for="social in socials"
            :key="social.name"
            :href="social.href"
            target="_blank"
            rel="noopener noreferrer"
            class="relative py-1 text-sm font-medium text-zinc-400 transition-colors hover:text-white after:absolute after:bottom-0 after:left-0 after:h-[2px] after:w-0 after:bg-white after:transition-all hover:after:w-full"
          >
            {{ social.name }}
          </a>
        </div>
      </div>

      <!-- RIGHT: CONTACT FORM -->
      <div
        class="bg-white p-8 text-zinc-900 dark:bg-zinc-900/50 dark:text-white sm:p-12 lg:w-3/5 lg:p-16"
      >
        <h3 class="mb-3 text-2xl font-bold tracking-tight">
          Tell me about your project.
        </h3>

        <p class="mb-10 text-sm leading-6 text-zinc-500 dark:text-zinc-400">
          Share your project details and I will get back to you as soon as
          possible.
        </p>

        <form class="space-y-8 sm:space-y-10" @submit.prevent="sendMessage">
          <!-- HONEYPOT -->
          <div class="hidden" aria-hidden="true">
            <input
              v-model="form.botcheck"
              type="checkbox"
              name="botcheck"
              tabindex="-1"
              autocomplete="off"
            />
          </div>

          <!-- NAME AND EMAIL -->
          <div class="grid grid-cols-1 gap-8 sm:gap-10 md:grid-cols-2">
            <div class="relative">
              <input
                id="contact-name"
                v-model="form.name"
                name="name"
                type="text"
                required
                maxlength="100"
                autocomplete="name"
                placeholder=" "
                :disabled="isSending"
                :class="inputClass"
              />

              <label for="contact-name" :class="labelClass"> Name </label>
            </div>

            <div class="relative">
              <input
                id="contact-email"
                v-model="form.email"
                name="email"
                type="email"
                required
                maxlength="254"
                autocomplete="email"
                placeholder=" "
                :disabled="isSending"
                :class="inputClass"
              />

              <label for="contact-email" :class="labelClass">
                Email Address
              </label>
            </div>
          </div>

          <!-- SUBJECT -->
          <div class="relative">
            <input
              id="contact-subject"
              v-model="form.subject"
              name="subject"
              type="text"
              required
              maxlength="150"
              placeholder=" "
              :disabled="isSending"
              :class="inputClass"
            />

            <label for="contact-subject" :class="labelClass"> Subject </label>
          </div>

          <!-- MESSAGE -->
          <div class="relative">
            <textarea
              id="contact-message"
              v-model="form.message"
              name="message"
              rows="4"
              required
              maxlength="4000"
              placeholder=" "
              :disabled="isSending"
              :class="[inputClass, 'resize-none']"
            ></textarea>

            <label for="contact-message" :class="labelClass">
              Project Details
            </label>
          </div>

          <!-- RESULT MESSAGE -->
          <div
            v-if="statusMessage"
            role="status"
            aria-live="polite"
            class="rounded-xl border px-5 py-4 text-sm leading-6"
            :class="
              status === 'success'
                ? 'border-green-200 bg-green-50 text-green-700 dark:border-green-500/20 dark:bg-green-500/10 dark:text-green-300'
                : 'border-red-200 bg-red-50 text-red-700 dark:border-red-500/20 dark:bg-red-500/10 dark:text-red-300'
            "
          >
            <div class="flex items-start gap-3">
              <svg
                class="mt-0.5 h-5 w-5 shrink-0"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  v-if="status === 'success'"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M5 13l4 4L19 7"
                />

                <path
                  v-else
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 9v4m0 4h.01M12 3a9 9 0 110 18 9 9 0 010-18z"
                />
              </svg>

              <span>{{ statusMessage }}</span>
            </div>
          </div>

          <!-- SUBMIT BUTTON -->
          <div class="pt-6 sm:pt-8">
            <button
              type="submit"
              :disabled="isSending"
              class="flex w-full items-center justify-center rounded-full bg-zinc-900 px-10 py-4 text-sm font-bold uppercase tracking-widest text-white shadow-lg transition-all duration-300 hover:-translate-y-1 hover:bg-blue-600 hover:shadow-xl disabled:cursor-not-allowed disabled:opacity-60 disabled:hover:translate-y-0 dark:bg-blue-600 dark:hover:bg-blue-500 sm:w-auto"
            >
              <svg
                v-if="isSending"
                class="mr-3 h-5 w-5 animate-spin"
                fill="none"
                viewBox="0 0 24 24"
              >
                <circle
                  class="opacity-25"
                  cx="12"
                  cy="12"
                  r="10"
                  stroke="currentColor"
                  stroke-width="4"
                />

                <path
                  class="opacity-75"
                  fill="currentColor"
                  d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"
                />
              </svg>

              <span>
                {{ isSending ? "Sending..." : "Send Message" }}
              </span>

              <svg
                v-if="!isSending"
                class="ml-3 h-5 w-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M14 5l7 7m0 0l-7 7m7-7H3"
                />
              </svg>
            </button>

            <p class="mt-4 text-xs leading-5 text-zinc-400 dark:text-zinc-500">
              Your inquiry is processed through Web3Forms and forwarded to my
              email.
            </p>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes slideUpFade {
  from {
    opacity: 0;
    transform: translateY(40px) scale(0.98);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.animate-slide-up {
  animation: slideUpFade 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@media (prefers-reduced-motion: reduce) {
  .animate-slide-up {
    animation: none;
    opacity: 1;
    transform: none;
  }
}
</style>
