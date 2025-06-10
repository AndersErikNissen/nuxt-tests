<template>
  <section class="p-index my-10">
    <div class="py-5">
      <h1 class="text-4xl">Slider</h1>
    </div>

    <div class="max-w-[1200px]">
      <SliderScaling :items="data.items" />
    </div>
  </section>
</template>

<script setup>
const data = {
  items: [
    {
      img: "https://images.unsplash.com/photo-1748882145961-536cc88fd117?q=80&w=2624&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      type: "Article",
      date: "25. November, 2024",
      title: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam efficitur scelerisque magna eu feugiat.",
    },
    {
      img: "https://images.unsplash.com/photo-1714418880871-22643a62660e?q=80&w=3648&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      type: "News",
      date: "13. January, 2022",
      title: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam efficitur scelerisque magna eu feugiat.",
    },
    {
      img: "https://images.unsplash.com/photo-1716149118354-2a9c46f26779?q=80&w=3987&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      type: "News",
      date: "09. May, 2023",
      title: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam efficitur scelerisque magna eu feugiat.",
    },
    {
      img: "https://images.unsplash.com/photo-1714418880871-22643a62660e?q=80&w=3648&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      type: "Article",
      date: "18. February, 2022",
      title: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam efficitur scelerisque magna eu feugiat.",
    },
  ],
};
</script>

<style lang="postcss"></style>
