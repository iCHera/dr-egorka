<template>
  <div class="card">
    <h1>🎂 С Днём Рождения, {{ name }}! 🎉</h1>
    <p>{{ message }}</p>
    <p> {{ message1 }} </p>

    <div class="buttons">
      <button @click="toggleMusic">
        {{ isPlaying ? "⏸ Остановить музыку" : "▶️ Воспроизвести музыку" }}
      </button>

      <button @click="launchConfetti">✨ Конфетти</button>
    </div>

      <div class="images">
    <img
      v-for="(img, index) in photos"
      :key="index"
      :src="img"
      alt="photo"
      @click="openImage(img)"
    />
  </div>

  <!-- Модалка полноэкранного просмотра -->
  <div v-if="selectedImage" class="modal" @click.self="closeImage">
    <button class="close-btn" @click="closeImage">✖</button>
    <img :src="selectedImage" alt="full" class="modal-img" />
  </div>

    <audio ref="audio" loop>
      <source src="/images/happy-birthday.mp3" type="audio/mpeg" />
      бля дебил на твоем браузере нет проигрывателя музыки.
    </audio>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import confetti from 'canvas-confetti'

const name = 'Егорка'
const message = 'Пусть каждый день будет ярким, как этот! 🎈'
const isPlaying = ref(false)
const audio = ref(null)

const message1 = `Братан, с днём ебучего рождения тебя! 🎉

Ты, блядь, представляешь вообще, насколько ты охуенный человек?  
Серьёзно, я иногда думаю — ну не может же один жирный уёбок быть настолько добрым, смешным, и при этом настоящим. А потом вспоминаю — это же ты, Егорка. Всё может.

Да, у тебя пузо, как у доброго Будды, но зато душа ещё больше.  
Ты умеешь выслушать, поддержать, поржать так, что слёзы катятся, и даже, сука, заставить поверить в себя, когда всё вокруг в пизду идёт.

Спасибо тебе за то, что ты есть. Не просто как "друг", а как брат, как тот, с кем и бухнуть, и помолчать, и поугарать, и в дерьме поваляться — всё можно, и всё по кайфу.

Желаю тебе, чтобы в жизни всё складывалось охуенно:  
— здоровья тебе, жиробас ты мой любимый (но давай уже чуть меньше колы и чуть больше движений, ага?)  
— денег столько, чтобы даже булки для бургера ты покупал из золота  
— и любви… ну такой, чтобы тебя любили не меньше, чем я тебя люблю (а это, блядь, планка высокая)`

const selectedImage = ref(null)

const openImage = (img) => {
  selectedImage.value = img
}

const closeImage = () => {
  selectedImage.value = null
}

const toggleMusic = () => {
  if (!audio.value) return
  if (isPlaying.value) {
    audio.value.pause()
  } else {
    audio.value.play()
  }
  isPlaying.value = !isPlaying.value
}

const launchConfetti = () => {
  confetti({
    particleCount: 100,
    spread: 70,
    origin: { y: 0.5 },
  })
}

const photos = [
  '/dr-egorka/images/friend1.jpg',
  '/dr-egorka/images/friend2.jpg',
  '/dr-egorka/images/friend3.jpg',
  '/dr-egorka/images/friend4.jpg',
  '/dr-egorka/images/friend5.jpg',
]
</script>

<style scoped>
.card {
  max-width: 700px;
  margin: 50px auto;
  padding: 2rem;
  border-radius: 12px;
  background: linear-gradient(to right, #ffecd2, #fcb69f);
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  animation: fadeIn 1s ease-in-out;
}

h1 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}

.buttons {
  margin-bottom: 1.5rem;
  display: flex;
  justify-content: center;
  gap: 1rem;
}

button {
  background: #ff6f61;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s ease;
}

button:hover {
  background: #e85c50;
}

.gallery {
  margin-top: 2rem;
}

.images {
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
}

.images img {
  width: 100px;
  border-radius: 8px;
  transition: transform 0.3s;
}

.images img:hover {
  transform: scale(1.05);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
