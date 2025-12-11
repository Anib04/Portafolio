<template>
  <UModal :title="theProyect?.title" :transition="true" >
    <template #body>
      <div class="flex justify-evenly gap-4 grow items-stretch h-full">
        
                    <div class="w-1/2 m-8">
                        <UCarousel
                            v-slot="{ item }"
                            :items="imagenesCarrousel"
                            loop
                            orientation="vertical"
                            :autoplay="{ delay: 2000 }"
                            :ui="{ item: 'basis-1/2', container: 'h-[250px]' }"
                        >
                            
                                <img :src="item" width="650" height="450" class="rounded-lg" :alt="props.theProyect?.title" />
                           
                        </UCarousel>
                    </div>
        
                    <div class="w-1/2 flex m-8">
                        <ol class="list-disc list-inside space-y-1 font-semibold ">
                            <li v-for="tech in theProyect?.technology" :key="tech" class="text-sm">
                            {{ tech }}
                            </li>
                        </ol>
                    </div>

        </div>
    </template>
    <template #footer>
      <div class="flex justify-around w-full">
        <UButton color="primary" :href="theProyect?.github" class="w-1/3 justify-center rounded-md my-1.5 px-4 py-3 bg-blue-500 transition delay-150 duration-300 ease-in-out hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500">Github</UButton>
        <UButton v-if="theProyect?.demo" color="primary" :href="theProyect?.demo" class="w-1/3 justify-center rounded-md my-1.5 px-4 py-3 bg-blue-500 transition delay-150 duration-300 ease-in-out hover:-translate-y-1 hover:scale-110 hover:bg-indigo-500">Demo</UButton>
      </div>

    </template>
  </UModal>
</template>

<script setup lang="ts">
import {  computed } from 'vue';
interface Proyect {
    title: string;
    srcImg: string;
    technology: Array<string>
    github?: string;
    demo?: string;    

}

const props = defineProps<{
    theProyect: Proyect | null;
}>();

// ... (dentro de < setup>)


const imagenesCarrousel = computed<string[]>(() => {
  const folderName = props.theProyect?.title.replace(/\s+/g, '_').toLowerCase();

  if (!folderName) {
    return [];
  }

  // 1. Forzar el tipo de los valores importados a string
  // Usamos as string para decirle a TypeScript que los valores de import: 'default' son URLs de string.
  const modules: Record<string, string> = import.meta.glob(
    '~/assets/img/**/*.png', 
    { eager: true, import: 'default' }
  ) as Record<string, string>;

  const files = Object.keys(modules)
    // 2. Filtrar para solo incluir las rutas de la carpeta actual
    .filter(path => path.includes(`/assets/img/${folderName}/`))
    
    // 3. Mapear para obtener la URL
    .map(path => modules[path])
    
    // 4. Filtrar y Aserción Final: ¡CLAVE!
    // Usamos el predicado de tipo para convencer a TypeScript de que eliminamos los undefined.
    .filter((item): item is string => typeof item === 'string'); // <-- 🚨 Filtrado y Aserción Fuerte

    console.log(files);
    
  return files;
});

// 2. Propiedad computada para obtener las imágenes de la carpeta

</script>