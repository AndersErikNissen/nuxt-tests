<template>
  <div class="c-slider-scaling" ref="component">
    <div class="p-5 mb-5 bg-amber-950 text-amber-50 rounded-2xl">
      <pre>{{ progresses }}</pre>
    </div>
    <div class="flex overflow-x-scroll items-end pb-5 bg-amber-50 rounded-2xl" ref="scroller">
      <div
        v-for="(item, index) in items"
        :key="item.title"
        class="item sticky left-0 bg-amber-50 rounded-2xl"
        :class="{ scaleable: index > 0, 'flex-[0_0_60%]': index === 0 }"
        :style="[
          index !== items.length - 1 ? '--progress-next:' + progresses[index] : '',
          index > 0 ? '--progress:' + progresses[index - 1] : '',
        ]"
        ref="item"
      >
        <img class="aspect-[4/3] object-cover rounded-2xl relative" :src="item.img" />
        <div class="p-4 overflow-hidden">
          <div class="item__text">
            <p class="opacity-60 py-2">{{ item.type }} - {{ item.date }}</p>
            <div class="text-2xl">
              <p class="item__text-scaleable">{{ item.title }}</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Enables us to scroll fully to the last element -->
      <div class="flex-[0_0_40%]" />
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  items: {
    type: Array,
    default: [],
  },
});

const scrollerRef = useTemplateRef("scroller");
const itemRefs = useTemplateRef("item");
const progresses = ref(props.items.map(() => 0).slice(1)); // slice since we don't need a progress for the first item
const index = ref(0);

function updateProgress() {
  const target = itemRefs.value[0].getBoundingClientRect().width;
  const currentIndex = index.value;
  let x = scrollerRef.value.scrollLeft;

  let progress = ((x - target * index.value) / target) * 100;

  if (progress >= 100) {
    progress = 100;
    index.value = Math.min(progresses.value.length - 1, index.value + 1);
  }

  if (0 >= progress) {
    progress = 0;
    index.value = Math.max(0, index.value - 1);
  }

  progresses.value[currentIndex] = progress;
  if (currentIndex !== index.value) progresses.value[index.value] = 100 - progress;
}

onMounted(() => {
  scrollerRef.value.addEventListener("scroll", updateProgress);
});
</script>

<style lang="postcss">
:where(.c-slider-scaling) {
  & .item {
    flex-shrink: 0;
    flex-grow: 0;

    &.scaleable {
      flex-basis: calc(40% + ((var(--progress, 0) / 10 * 2 * 1%)));

      .item__text-scaleable {
        min-height: calc((1em * (2 / 1.5)) * 2); /* a bit of "cheating" to avoid the layout shifting, when scaling... */

        font-size: calc(1em * calc(0.5 + (var(--progress, 0) * 0.005)));
      }
    }

    & .item__text {
      transform: translateY(calc(var(--progress-next, 0) * -1 * 1%));
    }
  }
}
</style>
