<template>
  <div id="app">
    <div class="scroll-container">
      <div class="content">
        <div class="box" ref="box">Scroll to transform me</div>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';

export default {
  name: 'App',
  setup() {
    const box = ref(null);

    onMounted(() => {
      const handleScroll = () => {
        const scrollPosition = window.scrollY;
        if (box.value) {
          if (scrollPosition >= 0 && scrollPosition < 400) {
            box.value.style.transform = 'rotate(0deg)';
            box.value.style.backgroundColor = '#3498db';
          } else if (scrollPosition >= 200 && scrollPosition < 600) {
            box.value.style.transform = 'rotate(45deg)';
            box.value.style.backgroundColor = '#2ecc71';
          } else if (scrollPosition >= 400 && scrollPosition < 800) {
            box.value.style.transform = 'rotate(90deg)';
            box.value.style.backgroundColor = '#e74c3c';
          } else if (scrollPosition >= 600 && scrollPosition < 1000) {
            box.value.style.transform = 'scale(1.5)';
            box.value.style.backgroundColor = '#f1c40f';
          } else if (scrollPosition >= 800 && scrollPosition < 1400) {
            box.value.style.transform = 'scale(2)';
            box.value.style.backgroundColor = '#9b59b6';
          } else if (scrollPosition >= 1000) {
            box.value.style.transform = 'translateY(100px)';
            box.value.style.backgroundColor = '#34495e';
          }
        }
      };

      window.addEventListener('scroll', handleScroll);

      // Clean up the event listener on unmount
      return () => {
        window.removeEventListener('scroll', handleScroll);
      };
    });

    return { box };
  }
};
</script>

<style scoped>
.scroll-container {
  height: 5000px;
  background: linear-gradient(to bottom, #ffffff, #000000);
}

.content {
  position: sticky;
  top: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.box {
  width: 100px;
  height: 100px;
  background-color: #3498db;
  transition: transform 0.5s, background-color 0.5s;
}
</style>
