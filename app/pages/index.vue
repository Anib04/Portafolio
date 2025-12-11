
<template>
    <myHeader />
    <section class="h-screen bg-[url(~/assets/img/bg.jpg)] bg-cover text-center flex items-center" ref="sectionRef">
        <UContainer class="flex justify-center items-center " >
            <UCard>
                    <h1 class="animate-typing overflow-hidden whitespace-nowrap border-r-4 border-r-white pr-5 text-5xl text-white font-bold">
                        Anibal Bello Desarrollador Web
                    </h1>
            </UCard>
        </UContainer>
    </section>
    <USeparator size="lg" />
    <section ref="sectionRef">
        <UContainer id="aboutMe" class="mt-10 flex items-stretch justify-evenly gap-x-6 h-screen mb-10 border-3 rounded-md p-8">
            <UCard class="grid bg-gray-800 p-4 rounded-lg shadow-lg" :class="[baseClass, 
                'delay-300', 
                isSectionVisible ? visibleClass : hiddenClass]">
                            <p class="text-lg text-white wrap" :class="[baseClass, 
                'delay-450', 
                isSectionVisible ? visibleClass : hiddenClass]" 
            >
                        Soy Anibal Bello, un Desarrollador Frontend
                        Con más de 2 años de experiencia, apasionado por construir soluciones web que sean tanto funcionales como elegantes. Mi especialización es el ecosistema moderno de JavaScript, y mi stack principal es Vue.js (Vue 3), TypeScript y Pinia.
                        <br>
                        Mi enfoque no es solo escribir código, sino construir sistemas. Disfruto el desafío de traducir diseños de alta fidelidad desde Figma  a componentes de código limpio y mantenible. Tengo experiencia demostrable en la implementación de librerías de componentes de nivel empresarial como Vuetify y Quasar Framework
                        <br>
                        En mis proyectos anteriores, me he centrado en la optimización del rendimiento, logrando reducir los tiempos de carga en un 25% mediante una gestión de estado eficiente con Pinia. También soy un firme defensor de la web inclusiva, habiendo mejorado la accesibilidad (WCAG) de aplicaciones en un 40%. Mi experiencia incluye la integración fluida con APIs REST y un dominio completo del control de versiones con Git.
                        <br>
                        Estoy acostumbrado a la cadencia del desarrollo profesional, trabajando en entornos Ágiles (Scrum/Kanban)  donde la colaboración, la comunicación efectiva y la entrega continua de valor son clave.
                    </p>
            </UCard>
            <img src="~/assets/img/IMG_20240122_094122_077.png" size="md" alt="Anibal Bello" class="rounded-full" :class="[baseClass, 
        'delay-600', 
        isSectionVisible ? visibleClass : hiddenClass]" />
        </UContainer>
    </section>   
    <USeparator size="lg" />
    <section ref="gridRef">
        <UContainer id="habilitys" class="mt-10 flex flex-col justify-center items-center gap-x-6 mb-10">
            <h2 class="text-4xl font-bold mb-1.5">Habilidades</h2>
            <div class="mt-5 flex gap-5 flex-wrap justify-center items-center content-center" >
                <UCard v-for="(language, index) in languages" class="w-1/5 p-4 flex flex-col justify-center items-center  transition-all duration-700 transform" :key="language.id"
                    :class="isGridVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'"
      :style="{ transitionDelay: `${index * 150}ms` }"
                >
                    <template #header>
                        <UIcon :name="language.icon" />
                            {{ language.name }}
                    </template>
                    <span>

                        {{ language.level }}
                    </span>
                </UCard>
            </div>
            
        </UContainer>
    </section>   
    <section ref="proyectRef">
    <UContainer id="proyects" class="mt-10 flex flex-col justify-center items-stretch gap-x-6 mb-10 h-screen" >
        <h2 class="text-4xl font-bold mb-1.5 text-center">Proyectos</h2>
        <div class="flex gap-10 wrap justify-evenly">
            <UCard v-for="(proyect, index) in proyects" :key="proyect.id"  class="grow w-1/4 items-stretch flex flex-col transition-all duration-700 transform" 
                    :class="isProyectVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'"
      :style="{ transitionDelay: `${index * 300}ms` }" >
      
                <template #header>
                    <span class="font-semibold">{{ proyect.title }}</span>
                </template>

                <div class="flex justify-center grow items-stretch h-full">
        
                    
                    <img :src="proyect.srcImg" :alt="proyect.title" class="object-cover w-full h-auto rounded-lg" />
        
                </div>
                <template #footer>
                    <UButton color="primary" class="w-full justify-center rounded-none px-4 py-3 bg-blue-500 transition delay-150 duration-300 ease-in-out hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500" @click="openModal(proyect)">Ver Proyecto</UButton>
                </template>
            </UCard>
        </div>
    </UContainer>
    </section>  
    <DescriptionModal v-model:open="showModal" :theProyect="proyectShow" ">

  </DescriptionModal> 
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