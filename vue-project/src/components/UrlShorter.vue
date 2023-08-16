<template>
    <div class="url-shortener">
        <h1>URL Shortener</h1>
        <input v-model="originalUrl" placeholder="Enter your URL" />
        <button @click="shortenUrl">Shorten</button>
        <p v-if="shortenedUrl">
        Shortened URL: <a :href="shortenedUrl" target="_blank">{{ shortenedUrl }}</a>
        </p>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';
import axios from 'axios';

const originalUrl = ref('');
const shortenedUrl = ref('');

const shortenUrl = async () => {
try {
    const response = await axios.post('YOUR_BACKEND_API_URL', { url: originalUrl.value });
    shortenedUrl.value = response.data.shortUrl;
} catch (error) {
    console.error('Error shortening URL:', error);
}
};
</script>
  
<style scoped>
.url-shortener {
max-width: 400px;
margin: 0 auto;
text-align: center;
}
</style>
  