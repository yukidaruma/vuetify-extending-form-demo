<template>
  <v-app>
    <v-main class="ma-8">
      <v-form v-model="isValid">
        <file-input ref="fileInput" :max-file-size="maxFileSize" />
      </v-form>

      <p>
        Is form valid? <b :class="isValid || 'red--text'">{{ isValid }}</b>
      </p>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import FileInput from './components/FileInput.vue';

export default Vue.extend({
  name: 'App',
  components: {
    FileInput,
  },
  data() {
    return {
      isValid: false,
      maxFileSize: 5 * 1024,
    };
  },
});
</script>
