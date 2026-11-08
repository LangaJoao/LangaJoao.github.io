<script setup>
import { ref } from 'vue'
defineProps({ screens: { type: Array, required: true }, title: { type: String, required: true }, portrait: Boolean })
const selected = ref(0)
const preview = ref(null)
function move(direction, count) { selected.value = (selected.value + direction + count) % count }
</script>

<template>
  <div class="water-gallery techstore-gallery" :class="{ 'portrait-gallery': portrait }">
    <button class="water-cover" type="button" :aria-label="`Ampliar ${title}: ${screens[selected].title}`" @click="preview.showModal()">
      <Transition name="gallery-fade"><img :key="screens[selected].src" :src="screens[selected].src" :alt="`${title} — ${screens[selected].title}`" loading="lazy"></Transition>
      <span class="expand-image"><i class="pi pi-expand" aria-hidden="true"></i> Ampliar</span>
    </button>
    <div class="gallery-caption"><span>{{ screens[selected].title }}</span><span>{{ String(selected + 1).padStart(2, '0') }} / {{ screens.length }}</span></div>
    <div class="water-thumbnails" :aria-label="`Imagens de ${title}`">
      <button v-for="(screen, index) in screens" :key="screen.src" type="button" :class="{ selected: selected === index }" :aria-pressed="selected === index" @click="selected = index">
        <img :src="screen.src" alt="" loading="lazy"><span>{{ screen.title }}</span>
      </button>
    </div>
  </div>
  <dialog ref="preview" class="image-dialog" :aria-label="`Galeria de ${title}`" @click="event => { if (event.target === preview) preview.close() }" @keydown.left.prevent="move(-1, screens.length)" @keydown.right.prevent="move(1, screens.length)">
    <div class="preview-toolbar"><span>{{ title }} · {{ screens[selected].title }} · {{ selected + 1 }}/{{ screens.length }}</span><button type="button" aria-label="Fechar imagem" autofocus @click="preview.close()"><i class="pi pi-times" aria-hidden="true"></i></button></div>
    <img :src="screens[selected].src" :alt="`${title} — ${screens[selected].title}`">
    <div class="preview-controls"><button type="button" @click="move(-1, screens.length)">← Anterior</button><button type="button" @click="move(1, screens.length)">Seguinte →</button></div>
  </dialog>
</template>
