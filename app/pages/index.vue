
<template>

    
    <myHeader />

    <section class="min-w-screen min-h-screen bg-[url(~/assets/img/bg.jpg)] bg-cover bg-center flex items-center justify-center p-4" ref="sectionRef">
        <UContainer class="w-full flex justify-center items-center">
            <UCard class="w-full max-w-4xl bg-opacity-90 backdrop-blur-sm"> 
                <h1 class="animate-typing overflow-hidden whitespace-nowrap border-r-4 border-r-white pr-2 text-md md:text-4xl text-white font-bold mx-auto w-fit lg:text-5xl">
                    Anibal Bello Desarrollador Frontend
                </h1>
            </UCard>
        </UContainer>
    </section>

    <USeparator size="lg" />

    <section ref="sectionRef" class="min-w-screen min-h-screen  py-20 bg-gray-900 ">
        <UContainer id="aboutMe" class="flex flex-col-reverse lg:flex-row items-center justify-between gap-10">
            
            <UCard class="w-full lg:w-2/3 bg-gray-800 p-6 rounded-lg shadow-xl border border-gray-700" 
                :class="[baseClass, 'delay-300', isSectionVisible ? visibleClass : hiddenClass]">
                
                <h3 class="text-2xl font-bold text-primary mb-4 block md:hidden">Sobre Mí</h3>
                
                <p class="text-base md:text-lg text-gray-300 leading-relaxed text-justify" 
                   :class="[baseClass, 'delay-450', isSectionVisible ? visibleClass : hiddenClass]">
                    Soy un desarrollador apasionado por la arquitectura de software limpia y escalable. Mi especialidad es Vue.js (Vue 3 + Composition API), donde combino la potencia de TypeScript y Pinia para construir aplicaciones robustas, modulares y fáciles de mantener.
                    <br>
                    Más allá de escribir código, me enfoco en la calidad del producto final: desde la optimización del rendimiento con Vite hasta la implementación de buenas prácticas de UI/UX. Me caracterizo por mi capacidad de adaptación rápida a nuevos entornos y mi enfoque proactivo para resolver desafíos técnicos complejos.
                    <br>
                    <span>Mi Stack Principal:</span> Vue.js, TypeScript, Tailwind CSS, Firebase, Git.
                </p>
            </UCard>

            <div class="w-48 h-48 md:w-80 md:h-80 flex-shrink-0" 
                 :class="[baseClass, 'delay-600', isSectionVisible ? visibleClass : hiddenClass]">
                 <img src="~/assets/img/IMG_20240122_094122_077.png" 
                     alt="Anibal Bello" 
                     class="w-full h-full object-cover rounded-full border-4 border-primary shadow-2xl" />
            </div>

        </UContainer>
    </section>   

    <USeparator size="lg" />

    <section ref="gridRef" class="min-w-screen min-h-screen  py-20 bg-gray-950">
        <UContainer id="habilitys" class="flex flex-col items-center">
            <h2 class="text-3xl md:text-4xl font-bold mb-8 text-white">Habilidades</h2>
            
            <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-4 w-full">
                <UCard v-for="(language, index) in languages" :key="language.id"
                    class="flex flex-col justify-center items-center text-center transition-all duration-700 hover:border-primary group" 
                    :class="isGridVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'"
                    :style="{ transitionDelay: `${index * 100}ms` }"
                >
                    <template #header>
                        <div class="flex flex-col items-center gap-2">
                            <UIcon :name="language.icon" class="w-8 h-8 md:w-10 md:h-10 text-gray-400 group-hover:text-primary transition-colors" />
                            <span class="font-bold text-sm md:text-base">{{ language.name }}</span>
                        </div>
                    </template>
                    <span class="text-xs text-gray-500 font-mono uppercase tracking-wider">
                        {{ language.level }}
                    </span>
                </UCard>
            </div>
            
        </UContainer>
    </section>   

    <section ref="proyectRef" class="min-w-screen min-h-screen  py-20 bg-gray-900">
        <UContainer id="proyects" class="min-h-screen flex flex-col w-full">
            <h2 class="text-3xl md:text-4xl font-bold mb-10 text-center text-white">Proyectos</h2>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <UCard v-for="(proyect, index) in proyects" :key="proyect.id"  
                    class="flex flex-col h-full transition-all duration-700 hover:shadow-primary/20 hover:shadow-xl" 
                    :class="isProyectVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'"
                    :style="{ transitionDelay: `${index * 200}ms` }" >
            
                    <template #header>
                        <div class="flex justify-between items-center">
                            <span class="font-bold text-lg truncate">{{ proyect.title }}</span>
                            </div>
                    </template>

                    <div class="relative w-full rounded-md bg-gray-800">
                        <img :src="proyect.srcImg" :alt="proyect.title" class="object-cover w-full h-full transition-transform duration-500 hover:scale-105" />
                    </div>
                    
                    <template #footer>
                        <UButton 
                            block
                            color="primary" 
                            variant="solid"
                            class="transition-transform active:scale-95" 
                            @click="openModal(proyect)"
                        >
                            Ver Detalles
                        </UButton>
                    </template>
                </UCard>
            </div>
        </UContainer>
    </section>  

    <LazyDescriptionModal v-model:open="showModal" :theProyect="proyectShow" />
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useElementVisibility } from "@vueuse/core";
import DescriptionModal from '@/components/descriptionModal.vue';
import myHeader from '@/components/myHeader.vue';

const showModal = ref(false);
const proyectShow = ref <Proyect | null>(null);

const sectionRef = ref(null)
const gridRef = ref(null)
const proyectRef = ref(null)

const isProyectVisible = useElementVisibility(proyectRef)
const isGridVisible = useElementVisibility(gridRef)
const isSectionVisible = useElementVisibility(sectionRef)

// Tip Senior: Define las clases base en variables para no ensuciar el HTML
const baseClass = "transition-all duration-700 transform"
const visibleClass = "opacity-100 translate-y-0"
const hiddenClass = "opacity-0 translate-y-10"


interface Language {
    id: number;
    name: string;
    level: string;
    icon: string;
}

interface Proyect {
    id: number;
    title: string;
    srcImg: string;
    technology: Array<string>
    github?: string;
    demo?: string;    
}

const languages: Language[] = [
    {id:1, name: 'JavaScript', level: 'Advanced', icon: 'simple-icons:javascript' },
    {id:2, name: 'TypeScript', level: 'Intermediate', icon: 'simple-icons:typescript' },
    {id:3, name: 'Vue.js', level: 'Advanced', icon: 'simple-icons:vuedotjs' },
    {id:4, name: 'Quasar', level: 'Advanced', icon: 'simple-icons:quasar' },
    {id:5, name: 'Vuetify', level: 'Advanced', icon: 'simple-icons:vuetify' },
    {id:6, name: 'Nuxt', level: 'Beginner', icon: 'simple-icons:nuxt' },
    {id:7, name: 'Firebase', level: 'Beginner', icon: 'simple-icons:firebase' },
    {id:8, name: 'HTML', level: 'Advanced', icon: 'simple-icons:html5' },
    {id:9, name: 'CSS', level: 'Advanced', icon: 'simple-icons:css' },
    {id:10, name: 'Tailwind', level: 'Intermediate', icon: 'simple-icons:tailwindcss' },
    {id:11, name: 'PHP', level: 'Beginner', icon: 'simple-icons:php' },
    {id:12, name: 'MySql', level: 'Beginner', icon: 'simple-icons:mysql' },
];

const proyects: Proyect[] = [
    {id:1, title: 'ToDo App', srcImg: "/img/toDo-1.png", technology: ['HTML', 'CSS', 'Javascript', 'Vue.js', 'Quasar', 'Pinia'], github: "https://github.com/Anib04/ToDo"},
    {id:2, title: 'Ecommerce', srcImg: "/img/ecommerce-1.png", technology: ['HTML', 'CSS', 'Javascript', 'Vue.js', 'Vuetify', 'Pinia', 'Firebase', 'Stripe'], github: "https://github.com/Anib04/E-Commerce", demo:"https://am-commerce.netlify.app/"},
    {id:3, title: 'Portafolio', srcImg: "/img/portafolio-1.png", technology: ['HTML', 'CSS', 'Typescript', 'Vue.js', 'Nuxt', 'Tailwind'], github:"https://github.com/Anib04/Portafolio"},
]


const openModal = (proyect: Proyect) => {
    showModal.value = true;
    proyectShow.value = proyect;
}

</script>
