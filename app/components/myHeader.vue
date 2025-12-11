<template>
  <UHeader >
    <template #title>
      <Logo class="h-6 w-auto" />
    </template>


    <template #right>
        <UTooltip text="Sobre mi">
        <UButton
          color="neutral"
          variant="ghost"
          to="#aboutMe"
          icon="line-md:account"
          aria-label="Sobre Mí"
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
      
      
      
    </template>

  </UHeader>
</template>

