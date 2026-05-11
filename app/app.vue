<template>
  <div class="birthday-container">
    <!-- Tampilan Kado (Muncul jika belum diklik) -->
    <transition name="bounce">
      <div v-if="!isOpened" class="gift-section" @click="openGift">
        <p class="text-ucapan">HAPPY 20TH BIRTHDAY🎉❤️</p>
        <p class="text-ucapan">SALMA TSANIATUL MUNAWAROH🥰</p>
        <p class="text-ucapan">14 April 2026</p>
        <div class="gift-box">🎁</div>
        <p class="click-text">Ada kado untukmu, klik untuk buka! ❤️</p>
      </div>
    </transition>

    <!-- Tampilan Terminal (Muncul setelah kado diklik) -->
    <transition name="fade">
      <div v-if="isOpened" class="terminal-box">
        <div v-for="(line, index) in displayedLines" :key="index" class="line">
          <span :class="{ 'highlight': line.includes('🎂') }">{{ line }}</span>
        </div>
        
        <div v-if="isTyping" class="line">
          <span>{{ currentText }}</span>
          <span class="cursor"></span>
        </div>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isOpened = ref(false); // Status apakah kado sudah dibuka
const isTyping = ref(false);
const displayedLines = ref([]);
const currentText = ref("");

const nama = "Sayangku"; 
const pesan = [
  `Halo ${nama}!`,
  "Hari ini adalah hari yang sangat spesial buat kamuuu...",
  "Aku cuma mau bilang...",
  "SELAMAT ULANG TAHUN SAYANGG! 🎂",
  "Semoga kamu selalu diberikan kesehatan dan selalu dilancarkan terus rezekinya SAYANG...❤️",
  "Maaf kalo akuu selalu bikin kamuu marah dengan setiap pertanyaan akuu, dan maaf juga kalo akuu selalu memperlihatkan sifat cemburu akuu kemarin kemarin meskipun akuu gatau kamu sadar atau engga disetiap akuu memperlihatkan sipat cemburu akuu. Dan maaf juga kalo akuu selalu buat kamuu kecewa sayanggg, akuu janji bakal berubah jadi lebih baik lagi buat kedepannya, ayoo kita jalani ini bersama sama lagi yahhh sayang dan kalo ada apa apa jangan lupa ceritain ke akuu sayanggg karena akuu akan selalu ada buat kamuuu...❤️",
  "Bahagia selalu sayanggg...❤️",
  "I WILL ALWAYS LOVE YOU SAYANG❤️",
];

const sleep = (ms) => new Promise(resolve => setTimeout(resolve, ms));

const openGift = () => {
  isOpened.value = true;
  isTyping.value = true;
  startTyping(); // Mulai mengetik setelah kado dibuka
};

const startTyping = async () => {
  await sleep(800); // Jeda sebentar setelah kado meledak
  for (let i = 0; i < pesan.length; i++) {
    const fullLine = pesan[i];
    currentText.value = "";
    
    for (let j = 0; j < fullLine.length; j++) {
      currentText.value += fullLine[j];
      await sleep(70); 
    }
    
    displayedLines.value.push(currentText.value);
    currentText.value = "";
    await sleep(500); 
  }
  isTyping.value = false;
};
</script>

<style scoped>
.birthday-container {
  background-color: #e0f2fe;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  margin: 0;
  font-family: 'Courier New', Courier, monospace;
  overflow: hidden;
}

/* Styling Gift Box */
.gift-section {
  text-align: center;
  cursor: pointer;
}

.gift-box {
  font-size: 120px;
  transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  display: inline-block;
}

.gift-box:hover {
  transform: scale(1.2) rotate(10deg);
}

.text-ucapan {
    color: #fb7185;
    position: center;
    font-weight: bold;
    font-size: 5vh;
    margin-top: 5px;
    margin-bottom: 5px;
    

}

.click-text {
  color: #fb7185;
  margin-top: 20px;
  font-weight: bold;
  animation: pulse 1.5s infinite;
}

/* Styling Terminal */
.terminal-box {
  background-color: rgba(255, 255, 255, 0.8);
  color: #374151;
  padding: 100px;
  border-radius: 15px;
  box-shadow: 0 20px 50px rgba(0,0,0,0.4);
  width: 90%;
  max-width: 500px;
  min-height: 250px;
  text-align: left;
  font-weight: bold;
  padding-top: 20px;
}

.cursor {
  display: inline-block;
  width: 10px;
  height: 1.2em;
  background-color: #000000;
  margin-left: 5px;
  vertical-align: middle;
  animation: blink 0.8s infinite;
}

/* Animasi */
@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

/* Transisi Vue */
.bounce-leave-active {
  animation: bounce-out 0.5s;
}
.fade-enter-active {
  transition: opacity 1s ease;
}
.fade-enter-from {
  opacity: 0;
}

@keyframes bounce-out {
  0% { transform: scale(1); }
  25% { transform: scale(1.2); }
  100% { transform: scale(0); }
}

.line {
  margin-bottom: 12px;
  line-height: 1.6;
}

.highlight {
  color: #ff0404;
  font-weight: bold;
}
</style>