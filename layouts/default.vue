<template>
  <div class="flex min-w-dvw min-h-dvh overflow-x-hidden">
    <AppSidebar class="basis-1/5" />
    <div class="basis-4/5 relative">
      <AppHeader />
      <slot />

      <!-- <AppFooter class="bottom-0 w-full" /> -->
    </div>
  </div>
</template>
