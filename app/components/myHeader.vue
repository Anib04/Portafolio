

<template>
  <UHeader  :toggle="{
      color: 'neutral',
    }">
    <template #title >
      <h2 >Anibal Bello</h2>
    </template>


    

    <template #right class="">
      <nav class="hidden lg:inline-flex space-x-2">

        <UTooltip text="Sobre mi">
          <UButton
          color="neutral"
          variant="ghost"
          to="#aboutMe"
          icon="line-md:account"
          aria-label="Sobre Mí"
          class=""
        >
            Sobre Mí
          </UButton>
      </UTooltip>

      <UTooltip text="Habilidades y Tecnologias">
        <UButton
          color="neutral"
          variant="ghost"
          to="#habilitys"
          icon="eos-icons:edge-computing"
          aria-label="Habilidades"
        >
            Habilidades
        </UButton>
      </UTooltip>

      <UTooltip text="Mis Proyectos">
        <UButton
        color="neutral"
        variant="ghost"
        to="#proyects"
        icon="octicon:project-16"
        aria-label="Proyectos"
        >
        Proyectos
      </UButton>
    </UTooltip>
  </nav>
    </template>
    <template #body>
      <UNavigationMenu :items="items" orientation="vertical" class="-mx-2.5" />
    </template>

  </UHeader>
</template>

<script setup lang="ts">
  
import type { NavigationMenuItem } from '@nuxt/ui';

  const items = computed<NavigationMenuItem[]>(() => [
  { label: 'Sobre Mí', icon: 'i-heroicons-user', to: '#aboutMe'  },
  { label: 'Habilidades', to: '#habilitys', icon: 'i-heroicons-bolt' },
  { label: 'Proyectos', to: '#proyects', icon: 'i-heroicons-folder' },
])
</script>