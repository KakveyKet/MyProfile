<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from "vue";

// ==========================================
// STATE
// ==========================================
const pricingSection = ref(null);
const isVisible = ref(false);
const selectedPoster = ref(null);
const previewCloseButton = ref(null);

let observer = null;
let previousFocusedElement = null;

// ==========================================
// CLOUDINARY SERVICE POSTERS
// ==========================================
const servicePosters = [
  {
    id: "website",
    title: "Website Design & Development",
    subtitle:
      "Professional websites for businesses, brands and content creators.",
    image:
      "https://res.cloudinary.com/e0brilgp/image/upload/v1793260576/photo_2026-10-29_14-55-59.jpg",
    alt: "Website design and development promotional poster",
    price: 250,
    label: "Web Development",
    accent: "purple",
    target: "business-website",
    features: [
      "Business Websites",
      "Blog & News",
      "Booking Websites",
      "Responsive Design",
    ],
  },
  {
    id: "pos",
    title: "POS System Development",
    subtitle: "Manage sales, stock, inventory and daily business operations.",
    image:
      "https://res.cloudinary.com/e0brilgp/image/upload/v1793260576/photo_2026-10-29_14-55-56.jpg",
    alt: "POS sales and inventory system promotional poster",
    price: 350,
    label: "Sales Management",
    accent: "orange",
    target: "pos-system",
    features: [
      "Sales Management",
      "Stock & Inventory",
      "Customer Management",
      "Reports & Analytics",
    ],
  },
  {
    id: "school",
    title: "School Management System",
    subtitle: "A centralized solution for academic and school administration.",
    image:
      "https://res.cloudinary.com/e0brilgp/image/upload/v1793260576/photo_2026-10-29_14-56-02.jpg",
    alt: "School management system promotional poster",
    price: 350,
    label: "Education System",
    accent: "blue",
    target: "school-system",
    features: [
      "Student & Teacher",
      "Class & Attendance",
      "Scores & Payments",
      "Inventory & Settings",
    ],
  },
];

// ==========================================
// PRICING PLANS
// ==========================================
const pricingPlans = [
  {
    id: "website-blog",
    name: "Website & Blog",
    category: "WEB DEVELOPMENT",
    price: 250,
    description:
      "Professional websites for individuals, bloggers and content creators.",
    features: [
      "Personal & Portfolio Website",
      "Blog & News Management",
      "Post Categories & Tags",
      "Modern Responsive Design",
      "Basic SEO Optimization",
      "Contact & Social Media Links",
      "Content Management",
    ],
    featured: false,
  },
  {
    id: "business-website",
    name: "Business Website",
    category: "BUSINESS SOLUTIONS",
    price: 250,
    description:
      "Modern business websites to showcase your products and services.",
    features: [
      "Company & Business Website",
      "Product & Service Showcase",
      "Responsive Mobile Design",
      "Contact & Inquiry Forms",
      "Basic SEO Optimization",
      "Admin & Content Management",
      "Custom Business Features",
    ],
    featured: true,
  },
  {
    id: "pos-system",
    name: "POS System",
    category: "SALES MANAGEMENT",
    price: 350,
    description:
      "Custom sales and inventory solutions for shops, cafes and businesses.",
    features: [
      "Sales & Product Management",
      "Stock Management",
      "Inventory Management",
      "Customer Management",
      "Sales Reports & Analytics",
      "User & Role Management",
      "Dashboard & Settings",
    ],
    featured: false,
  },
  {
    id: "school-system",
    name: "School Management",
    category: "EDUCATION SYSTEM",
    price: 350,
    description: "Custom software for schools and training centers.",
    features: [
      "Student & Teacher Management",
      "Class & Academic Management",
      "Attendance & Schedule Management",
      "Student Scores & Permissions",
      "Student Payment Management",
      "Book & Inventory Management",
      "User & System Management",
    ],
    featured: false,
  },
];

const commonFeatures = [
  "Project Consultation",
  "Basic System Training",
  "Deployment Guidance",
];

// ==========================================
// CONTACT
// ==========================================
const phoneNumber = "096 763 7609";
const phoneLink = "tel:+855967637609";

// ==========================================
// STYLES FOR SERVICE TAGS
// ==========================================
const accentClasses = {
  purple: {
    label:
      "bg-purple-50 text-purple-700 dark:bg-purple-500/10 dark:text-purple-300",
    button: "bg-purple-600 hover:bg-purple-700 text-white",
    dot: "bg-purple-500",
  },
  orange: {
    label:
      "bg-orange-50 text-orange-700 dark:bg-orange-500/10 dark:text-orange-300",
    button: "bg-orange-500 hover:bg-orange-600 text-white",
    dot: "bg-orange-500",
  },
  blue: {
    label: "bg-blue-50 text-blue-700 dark:bg-blue-500/10 dark:text-blue-300",
    button: "bg-blue-600 hover:bg-blue-700 text-white",
    dot: "bg-blue-500",
  },
};

// ==========================================
// POSTER PREVIEW
// ==========================================
async function openPoster(poster) {
  if (typeof document !== "undefined") {
    previousFocusedElement = document.activeElement;
  }

  selectedPoster.value = poster;
  await nextTick();
  previewCloseButton.value?.focus();
}

async function closePoster() {
  selectedPoster.value = null;
  await nextTick();
  previousFocusedElement?.focus?.();
}

function handleKeyDown(event) {
  if (event.key === "Escape" && selectedPoster.value) {
    closePoster();
  }
}

// ==========================================
// SCROLL OBSERVER
// ==========================================
onMounted(() => {
  window.addEventListener("keydown", handleKeyDown);

  if (!("IntersectionObserver" in window)) {
    isVisible.value = true;
    return;
  }

  observer = new IntersectionObserver(
    (entries) => {
      if (entries[0]?.isIntersecting) {
        isVisible.value = true;
        observer?.disconnect();
        observer = null;
      }
    },
    { threshold: 0.08 },
  );

  if (pricingSection.value) {
    observer.observe(pricingSection.value);
  } else {
    isVisible.value = true;
  }
});

onBeforeUnmount(() => {
  observer?.disconnect();
  window.removeEventListener("keydown", handleKeyDown);
});
</script>

<template>
  <section
    id="pricing"
    ref="pricingSection"
    class="scroll-mt-24 sm:scroll-mt-32 transition-colors duration-500"
  >
    <!-- ================================== -->
    <!-- HEADER -->
    <!-- ================================== -->
    <div
      class="mb-12 text-center sm:mb-14"
      :class="isVisible ? 'animate-slide-up' : 'opacity-0'"
    >
      <span
        class="mb-4 inline-flex items-center gap-2 rounded-full border border-blue-200 bg-blue-50 px-4 py-2 text-[10px] font-bold uppercase tracking-[0.2em] text-blue-600 dark:border-blue-500/20 dark:bg-blue-500/10 dark:text-blue-400"
      >
        <span class="h-2 w-2 rounded-full bg-blue-500"></span>
        What I Build
      </span>

      <h2
        class="text-3xl font-extrabold tracking-tight text-zinc-900 dark:text-white sm:text-4xl"
      >
        My Development
        <span
          class="bg-gradient-to-r from-blue-600 to-cyan-500 bg-clip-text text-transparent"
        >
          Services.
        </span>
      </h2>

      <p
        class="mx-auto mt-4 max-w-2xl text-sm leading-7 text-zinc-500 dark:text-zinc-400 sm:text-base"
      >
        From professional websites to custom management systems, I develop
        practical software solutions tailored to your business needs.
      </p>
    </div>

    <!-- ================================== -->
    <!-- SERVICE PROMOTIONAL GALLERY -->
    <!-- ================================== -->
    <div
      class="mx-auto grid max-w-7xl grid-cols-1 gap-7 md:grid-cols-2 xl:grid-cols-3"
    >
      <article
        v-for="(service, index) in servicePosters"
        :key="service.id"
        class="group flex flex-col overflow-hidden rounded-[2rem] border border-zinc-200/80 bg-white shadow-lg shadow-zinc-200/30 transition-all duration-300 hover:-translate-y-1 hover:shadow-xl dark:border-zinc-800 dark:bg-zinc-900 dark:shadow-none"
        :class="isVisible ? 'animate-slide-up' : 'opacity-0'"
        :style="{
          animationDelay: `${index * 120 + 100}ms`,
        }"
      >
        <!-- FULL POSTER IMAGE -->
        <button
          type="button"
          class="relative block w-full overflow-hidden bg-zinc-100 text-left dark:bg-zinc-800"
          :aria-label="`Preview ${service.title} poster`"
          @click="openPoster(service)"
        >
          <img
            :src="service.image"
            :alt="service.alt"
            loading="lazy"
            decoding="async"
            width="750"
            height="1000"
            class="aspect-[3/4] w-full object-contain transition-transform duration-500 group-hover:scale-[1.015]"
          />

          <!-- HOVER OVERLAY -->
          <span
            class="absolute inset-0 flex items-center justify-center bg-zinc-950/0 transition-colors duration-300 group-hover:bg-zinc-950/30"
          >
            <span
              class="flex translate-y-2 items-center gap-2 rounded-full bg-white/95 px-5 py-3 text-xs font-bold text-zinc-900 opacity-0 shadow-xl transition-all duration-300 group-hover:translate-y-0 group-hover:opacity-100 group-focus-within:opacity-100"
            >
              <svg
                class="h-4 w-4"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 3h6v6m0-6l-7 7M9 21H3v-6m0 6l7-7"
                />
              </svg>
              View Full Poster
            </span>
          </span>
        </button>

        <!-- SERVICE DETAILS -->
        <div class="flex flex-1 flex-col p-6 sm:p-7">
          <div class="mb-4 flex items-center justify-between gap-2">
            <span
              class="inline-flex items-center gap-2 rounded-full px-3 py-1.5 text-[10px] font-bold uppercase tracking-wider"
              :class="accentClasses[service.accent].label"
            >
              <span
                class="h-1.5 w-1.5 rounded-full"
                :class="accentClasses[service.accent].dot"
              ></span>
              {{ service.label }}
            </span>

            <span class="text-sm font-extrabold text-zinc-900 dark:text-white">
              ${{ service.price }}+
            </span>
          </div>

          <h3
            class="text-lg font-bold tracking-tight text-zinc-900 dark:text-white"
          >
            {{ service.title }}
          </h3>

          <p
            class="mt-3 min-h-12 text-sm leading-6 text-zinc-500 dark:text-zinc-400"
          >
            {{ service.subtitle }}
          </p>

          <!-- FEATURE TAGS -->
          <div class="mt-5 flex flex-wrap gap-2">
            <span
              v-for="feature in service.features"
              :key="feature"
              class="rounded-lg border border-zinc-200 bg-zinc-50 px-3 py-2 text-[11px] font-medium text-zinc-600 dark:border-zinc-700 dark:bg-zinc-800 dark:text-zinc-300"
            >
              {{ feature }}
            </span>
          </div>

          <!-- ACTION BUTTONS -->
          <div class="mt-auto flex items-center gap-3 pt-7">
            <a
              :href="`#${service.target}`"
              class="flex flex-1 items-center justify-center rounded-full px-4 py-3.5 text-xs font-bold transition-colors"
              :class="accentClasses[service.accent].button"
            >
              View Pricing
            </a>

            <a
              href="#contact"
              class="flex flex-1 items-center justify-center rounded-full border border-zinc-200 px-4 py-3.5 text-xs font-bold text-zinc-700 transition-colors hover:bg-zinc-100 dark:border-zinc-700 dark:text-white dark:hover:bg-zinc-800"
            >
              Contact Me
            </a>
          </div>
        </div>
      </article>
    </div>

    <!-- ================================== -->
    <!-- PRICING SECTION TITLE -->
    <!-- ================================== -->
    <div class="mb-10 mt-20 text-center">
      <span
        class="text-[11px] font-bold uppercase tracking-[0.2em] text-blue-600 dark:text-blue-400"
      >
        Investment & Pricing
      </span>

      <h2
        class="mt-3 text-3xl font-extrabold tracking-tight text-zinc-900 dark:text-white sm:text-4xl"
      >
        Simple & Transparent Pricing.
      </h2>

      <p
        class="mx-auto mt-4 max-w-2xl text-sm leading-7 text-zinc-500 dark:text-zinc-400"
      >
        Select the service that fits your goals. Every project can be customized
        based on your requirements.
      </p>
    </div>

    <!-- ================================== -->
    <!-- PRICING CARDS -->
    <!-- ================================== -->
    <div
      class="mx-auto grid max-w-7xl grid-cols-1 items-stretch gap-6 md:grid-cols-2 xl:grid-cols-4"
    >
      <article
        v-for="(plan, index) in pricingPlans"
        :id="plan.id"
        :key="plan.id"
        class="relative flex scroll-mt-32 flex-col rounded-[2rem] border p-7 transition-all duration-300 sm:p-8"
        :class="[
          isVisible ? 'animate-slide-up' : 'opacity-0',
          plan.featured
            ? 'border-zinc-800 bg-zinc-900 text-white shadow-2xl shadow-zinc-900/15 dark:border-zinc-700 dark:bg-zinc-800'
            : 'border-zinc-200 bg-white text-zinc-900 shadow-lg shadow-zinc-200/30 hover:-translate-y-1 dark:border-zinc-800 dark:bg-zinc-900 dark:text-white dark:shadow-none',
        ]"
        :style="{
          animationDelay: `${index * 100 + 100}ms`,
        }"
      >
        <!-- FEATURED LABEL -->
        <div
          v-if="plan.featured"
          class="absolute -top-3 left-1/2 -translate-x-1/2 whitespace-nowrap rounded-full bg-gradient-to-r from-blue-600 to-cyan-500 px-4 py-1.5 text-[10px] font-bold uppercase tracking-wider text-white shadow-md"
        >
          Featured Service
        </div>

        <p
          class="mb-3 text-[10px] font-bold uppercase tracking-[0.18em]"
          :class="
            plan.featured ? 'text-blue-400' : 'text-blue-600 dark:text-blue-400'
          "
        >
          {{ plan.category }}
        </p>

        <h3
          class="text-xl font-bold tracking-tight"
          :class="
            plan.featured ? 'text-white' : 'text-zinc-900 dark:text-white'
          "
        >
          {{ plan.name }}
        </h3>

        <p
          class="mt-3 min-h-20 text-sm leading-6"
          :class="
            plan.featured ? 'text-zinc-400' : 'text-zinc-500 dark:text-zinc-400'
          "
        >
          {{ plan.description }}
        </p>

        <!-- PRICE -->
        <div class="mb-6 mt-6">
          <p
            class="mb-2 text-[11px] font-medium"
            :class="
              plan.featured
                ? 'text-zinc-400'
                : 'text-zinc-500 dark:text-zinc-400'
            "
          >
            Starting from
          </p>

          <div class="flex items-baseline gap-1">
            <span class="text-2xl font-bold text-zinc-400"> $ </span>

            <span
              class="text-5xl font-extrabold tracking-tight"
              :class="
                plan.featured ? 'text-white' : 'text-zinc-900 dark:text-white'
              "
            >
              {{ plan.price }}
            </span>

            <span class="ml-1 text-xs text-zinc-400"> / project </span>
          </div>
        </div>

        <div
          class="mb-6 border-t border-dashed"
          :class="
            plan.featured
              ? 'border-zinc-700'
              : 'border-zinc-200 dark:border-zinc-700'
          "
        ></div>

        <!-- FEATURES -->
        <p
          class="mb-5 text-[11px] font-bold uppercase tracking-wider"
          :class="
            plan.featured ? 'text-zinc-300' : 'text-zinc-700 dark:text-zinc-300'
          "
        >
          Available Features
        </p>

        <ul class="mb-8 flex-1 space-y-4">
          <li
            v-for="feature in plan.features"
            :key="feature"
            class="flex items-start gap-3"
          >
            <svg
              class="mt-0.5 h-5 w-5 shrink-0"
              :class="
                plan.featured
                  ? 'text-blue-400'
                  : 'text-blue-600 dark:text-blue-400'
              "
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              />
            </svg>

            <span
              class="text-sm font-medium leading-5"
              :class="
                plan.featured
                  ? 'text-zinc-300'
                  : 'text-zinc-600 dark:text-zinc-300'
              "
            >
              {{ feature }}
            </span>
          </li>
        </ul>

        <!-- INCLUDED SERVICES -->
        <div
          class="border-t border-dashed pt-6"
          :class="
            plan.featured
              ? 'border-zinc-700'
              : 'border-zinc-200 dark:border-zinc-700'
          "
        >
          <p
            class="mb-4 text-[10px] font-bold uppercase tracking-widest text-zinc-400"
          >
            Included Services
          </p>

          <ul class="mb-8 space-y-3">
            <li
              v-for="item in commonFeatures"
              :key="item"
              class="flex items-center gap-3"
            >
              <svg
                class="h-4 w-4 shrink-0 text-blue-500"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                />
              </svg>

              <span
                class="text-xs"
                :class="
                  plan.featured
                    ? 'text-zinc-400'
                    : 'text-zinc-500 dark:text-zinc-400'
                "
              >
                {{ item }}
              </span>
            </li>
          </ul>

          <a
            href="#contact"
            class="flex w-full items-center justify-center gap-2 rounded-full py-4 text-xs font-bold uppercase tracking-wider transition-colors"
            :class="
              plan.featured
                ? 'bg-blue-600 text-white hover:bg-blue-500'
                : 'bg-zinc-900 text-white hover:bg-blue-600 dark:bg-white dark:text-zinc-900 dark:hover:bg-blue-100'
            "
          >
            Get Started

            <svg
              class="h-4 w-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 12h14m-6-6l6 6-6 6"
              />
            </svg>
          </a>
        </div>
      </article>
    </div>

    <!-- ================================== -->
    <!-- PRICING NOTE -->
    <!-- ================================== -->
    <div
      class="mx-auto mt-10 max-w-4xl rounded-2xl border border-zinc-200 bg-zinc-50/70 p-6 text-center dark:border-zinc-800 dark:bg-zinc-900/50"
    >
      <p class="text-xs leading-7 text-zinc-500 dark:text-zinc-400">
        <strong class="text-zinc-800 dark:text-zinc-200">
          Pricing Information:
        </strong>

        All prices are starting rates in USD. Available features are configured
        according to the agreed project scope. Advanced integrations, hosting,
        domains, third-party services and ongoing maintenance may require
        additional fees.
      </p>
    </div>

    <!-- ================================== -->
    <!-- CUSTOM SYSTEM CTA -->
    <!-- ================================== -->
    <div
      class="relative mx-auto mt-12 max-w-5xl overflow-hidden rounded-[2rem] border border-zinc-200 bg-white p-8 dark:border-zinc-800 dark:bg-zinc-900 sm:p-10"
    >
      <div
        class="pointer-events-none absolute -right-20 -top-20 h-60 w-60 rounded-full bg-blue-500/10 blur-3xl"
      ></div>

      <div
        class="relative flex flex-col items-start justify-between gap-7 md:flex-row md:items-center"
      >
        <div class="max-w-xl">
          <p
            class="mb-3 text-[11px] font-bold uppercase tracking-widest text-blue-600 dark:text-blue-400"
          >
            Custom Development
          </p>

          <h3
            class="text-2xl font-extrabold tracking-tight text-zinc-900 dark:text-white"
          >
            Need a Custom Management System?
          </h3>

          <p class="mt-3 text-sm leading-7 text-zinc-500 dark:text-zinc-400">
            I build custom dashboards, internal business tools and web
            applications. Management systems start from $350, depending on the
            required functionality.
          </p>
        </div>

        <a
          href="#contact"
          class="inline-flex shrink-0 items-center justify-center gap-2 rounded-full bg-gradient-to-r from-blue-600 to-cyan-500 px-7 py-4 text-xs font-bold uppercase tracking-wider text-white transition-all hover:shadow-lg"
        >
          Request a Quote
        </a>
      </div>
    </div>

    <!-- ================================== -->
    <!-- CONTACT -->
    <!-- ================================== -->
    <div class="mt-10 text-center">
      <p class="text-sm text-zinc-500 dark:text-zinc-400">
        Have a project in mind? Let's discuss it.
      </p>

      <p class="mt-2 text-sm">
        <span class="text-zinc-500 dark:text-zinc-400">
          Telegram / Phone:
        </span>

        <a
          :href="phoneLink"
          class="ml-1 font-bold text-blue-600 hover:underline dark:text-blue-400"
        >
          {{ phoneNumber }}
        </a>
      </p>
    </div>

    <!-- ================================== -->
    <!-- FULL IMAGE PREVIEW MODAL -->
    <!-- ================================== -->
    <Teleport to="body">
      <div
        v-if="selectedPoster"
        class="fixed inset-0 z-[9999] flex items-center justify-center bg-black/85 p-3 backdrop-blur-sm sm:p-8"
        role="dialog"
        aria-modal="true"
        :aria-label="`${selectedPoster.title} poster preview`"
        @click.self="closePoster"
      >
        <div class="relative flex max-h-[95vh] max-w-3xl flex-col items-center">
          <button
            ref="previewCloseButton"
            type="button"
            class="absolute right-3 top-3 z-10 flex h-10 w-10 items-center justify-center rounded-full bg-zinc-900/80 text-white transition-colors hover:bg-zinc-700"
            aria-label="Close poster preview"
            @click="closePoster"
          >
            <svg
              class="h-5 w-5"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>

          <img
            :src="selectedPoster.image"
            :alt="selectedPoster.alt"
            class="max-h-[85vh] max-w-full rounded-xl object-contain shadow-2xl"
          />

          <a
            href="#contact"
            class="mt-4 rounded-full bg-blue-600 px-6 py-3 text-xs font-bold text-white transition-colors hover:bg-blue-500"
            @click="closePoster"
          >
            Discuss This Project
          </a>
        </div>
      </div>
    </Teleport>
  </section>
</template>

<style scoped>
@keyframes slideUpFade {
  from {
    opacity: 0;
    transform: translateY(30px) scale(0.98);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.animate-slide-up {
  animation: slideUpFade 0.7s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@media (prefers-reduced-motion: reduce) {
  .animate-slide-up {
    animation: none;
    opacity: 1;
    transform: none;
  }

  .group img {
    transition: none;
  }
}
</style>
