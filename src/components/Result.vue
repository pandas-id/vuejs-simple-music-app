<script setup>
import { ref } from 'vue'

defineProps(['trackList'])
defineEmits(['play'])

const currentAudio = ref('')
const currentButton = ref('')

const iconToPause = () => {
  currentButton.value.classList.remove('bi-play-circle')
  currentButton.value.classList.add('bi-pause-circle')
}

const iconToPlay = () => {
  currentButton.value.classList.remove('bi-pause-circle')
  currentButton.value.classList.add('bi-play-circle')
}

const playAudio = (e) => {
  const selectedAudio = e.target.querySelector('audio')
  const selectedButton = e.target

  if (currentAudio.value !== '') {
    if (currentAudio.value === selectedAudio) {
      currentAudio.value.pause()
      iconToPlay()
      return
    }

    currentAudio.value.pause()
    iconToPlay()

    currentAudio.value = selectedAudio
    currentAudio.value.play()

    currentButton.value = selectedButton
    iconToPause()
  } else {
    currentAudio.value = selectedAudio
    currentAudio.value.play()

    currentButton.value = selectedButton
    iconToPause()
  }

}
</script>

<template>
  <div class="list-group">
    <a v-for="track in trackList || []" class="list-group-item list-group-item-action" aria-current="false">
      <div class="d-flex w-100 justify-content-between">
        <p class="mb-1 fw-semibold">{{track['title']}}</p>
<i @click="playAudio" class="bi-play-circle" style="font-size: 1.5rem;" data-play="false">
        <audio :src="track['preview']" preload="none"></audio>
        </i>
      </div>
      <small class="text-secondary">{{ track['artist']['name']}}</small>
    </a>
  </div>
</template>
