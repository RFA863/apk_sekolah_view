<template>
  <div class="flex min-w-dvw min-h-dvh">
    <AppSidebar class="basis-1/5" />
    <div class="basis-4/5">
      <AppHeader />
      <slot />
      <AppFooter class="absolute bottom-0" />
    </div>
  </div>
</template>
