<template>
  <div class="bg-primary">
    <nuxt />
  </div>
</template>

<style>
body {
  overflow-y: hidden;
}

#sidenav {
  background-color: rgba(94,187,65, 1);
}

.custom-scroll::-webkit-scrollbar-track
{
  background-color: rgba(0, 0, 0, 0.1)
}

.custom-scroll::-webkit-scrollbar
{
  width: 10px;
  background-color:rgba(0, 0, 0, 0.1);
}

.custom-scroll::-webkit-scrollbar-thumb
{
  background-color: rgba(0, 0, 0, 0.2)
}
</style>
