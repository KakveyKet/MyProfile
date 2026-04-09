<script setup>
import { ref, onMounted } from 'vue'

// 1. Setup Intersection Observer for scroll animations
const pricingSection = ref(null)
const isVisible = ref(false)

onMounted(() => {
    const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
            isVisible.value = true
            observer.disconnect()
        }
    }, {
        threshold: 0.1
    })

    if (pricingSection.value) {
        observer.observe(pricingSection.value)
    }
})

// 2. Pricing Data
const pricingPlans = [
    {
        name: 'Starter',
        price: '150',
        description: 'Perfect for individuals and content creators.',
        features: [
            'Professional Personal Website',
            'Custom Blog Setup',
            'Responsive Mobile Design',
            'Basic SEO Optimization'
        ],
        isPopular: false,
        theme: 'light'
    },
    {
        name: 'Business',
        price: '250',
        description: 'Complete platforms for sales and service bookings.',
        features: [
            'E-Commerce Store setup',
            'Service / Hotel Booking System',
            'Stripe & PayPal Integration',
            'Bakong & Internal Pay Setup'
        ],
        isPopular: true,
        theme: 'dark'
    },
    {
        name: 'System',
        price: '320',
        description: 'Advanced management systems and internal tools.',
        features: [
            'POS (Point of Sale) System',
            'School Management System',
            'HRMS (HR Management)',
            'Custom Business Workflows'
        ],
        isPopular: false,
        theme: 'light'
    }
]

const commonFeatures = [
    'Free comprehensive training',
    'Free system maintenance',
    'Business solution consulting'
]
</script>

<template>
    <section id="pricing" class="scroll-mt-24 sm:scroll-mt-32" ref="pricingSection">

        <!-- Section Header -->
        <div class="mb-12 sm:mb-16 text-center opacity-0" :class="{ 'animate-slide-up': isVisible }"
            style="animation-delay: 0ms;">
            <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-2 sm:mb-3">Investment</h2>
            <h3 class="text-3xl sm:text-4xl font-extrabold text-zinc-900 tracking-tight">Transparent Pricing.</h3>
            <p class="mt-4 text-zinc-500 font-light max-w-2xl mx-auto">
                High-quality development services tailored to your specific business needs, with no hidden fees.
            </p>
        </div>

        <!-- Pricing Grid -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-6xl mx-auto">

            <div v-for="(plan, index) in pricingPlans" :key="plan.name"
                class="relative flex flex-col p-8 sm:p-10 rounded-[2.5rem] transition-all duration-500 opacity-0"
                :class="[
                    { 'animate-slide-up': isVisible },
                    plan.theme === 'dark'
                        ? 'bg-zinc-900 text-white shadow-2xl shadow-zinc-900/20 scale-100 md:scale-105 z-10'
                        : 'bg-white/80 backdrop-blur-xl border border-zinc-200/60 shadow-lg shadow-zinc-200/40 hover:-translate-y-2'
                ]" :style="{ animationDelay: `${index * 150 + 150}ms` }">
                <!-- Popular Badge -->
                <div v-if="plan.isPopular"
                    class="absolute -top-4 left-1/2 -translate-x-1/2 bg-gradient-to-r from-blue-500 to-cyan-500 text-white text-[10px] font-bold uppercase tracking-widest py-1.5 px-4 rounded-full shadow-md">
                    Most Popular
                </div>

                <!-- Plan Header -->
                <div class="mb-8">
                    <h4 class="text-lg font-semibold mb-2"
                        :class="plan.theme === 'dark' ? 'text-zinc-300' : 'text-zinc-500'">{{ plan.name }}</h4>
                    <div class="flex items-baseline gap-1">
                        <span class="text-3xl font-bold"
                            :class="plan.theme === 'dark' ? 'text-zinc-400' : 'text-zinc-400'">$</span>
                        <span class="text-5xl font-extrabold tracking-tight"
                            :class="plan.theme === 'dark' ? 'text-white' : 'text-zinc-900'">{{ plan.price }}</span>
                        <span class="text-sm font-medium ml-1"
                            :class="plan.theme === 'dark' ? 'text-zinc-500' : 'text-zinc-400'">/project</span>
                    </div>
                    <p class="mt-4 text-sm font-light leading-relaxed h-10"
                        :class="plan.theme === 'dark' ? 'text-zinc-400' : 'text-zinc-500'">
                        {{ plan.description }}
                    </p>
                </div>

                <!-- Specific Features -->
                <ul class="space-y-4 mb-8 flex-1">
                    <li v-for="feature in plan.features" :key="feature" class="flex items-start gap-3">
                        <svg class="w-5 h-5 shrink-0 mt-0.5"
                            :class="plan.theme === 'dark' ? 'text-blue-400' : 'text-blue-600'" fill="none"
                            stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7">
                            </path>
                        </svg>
                        <span class="text-sm font-medium"
                            :class="plan.theme === 'dark' ? 'text-zinc-200' : 'text-zinc-700'">{{ feature }}</span>
                    </li>
                </ul>

                <!-- Divider -->
                <div class="w-full border-t border-dashed mb-6"
                    :class="plan.theme === 'dark' ? 'border-zinc-700' : 'border-zinc-200'"></div>

                <!-- Common Included Features -->
                <div class="mb-10">
                    <p class="text-[11px] font-bold uppercase tracking-widest mb-4"
                        :class="plan.theme === 'dark' ? 'text-zinc-500' : 'text-zinc-400'">Included in all plans:</p>
                    <ul class="space-y-3">
                        <li v-for="common in commonFeatures" :key="common" class="flex items-center gap-3">
                            <svg class="w-4 h-4 shrink-0 text-green-500" fill="none" stroke="currentColor"
                                viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                            <span class="text-xs font-medium"
                                :class="plan.theme === 'dark' ? 'text-zinc-400' : 'text-zinc-500'">{{ common }}</span>
                        </li>
                    </ul>
                </div>

                <!-- CTA Button -->
                <a href="#contact"
                    class="w-full py-4 rounded-full text-sm font-bold uppercase tracking-widest text-center transition-all duration-300"
                    :class="plan.theme === 'dark' ? 'bg-white text-zinc-900 hover:bg-zinc-200' : 'bg-zinc-900 text-white hover:bg-zinc-800'">
                    Get Started
                </a>

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
    animation: slideUpFade 0.7s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
</style>