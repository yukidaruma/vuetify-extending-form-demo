<template>
  <div>
    <v-cloak @drop.prevent="addDropFile" @dragover.prevent>
      <v-file-input ref="fileInput" @change="handleFileChange" />
      <p>
        Current file size is <b>{{ JSON.stringify(fileSize) }}</b> bytes
      </p>
      <p>
        Maximum file size is <b>{{ maxFileSize }}</b> bytes
      </p>
      <p>
        Does my file exceed max file size? <b>{{ hasError }}</b>
      </p>
    </v-cloak>
  </div>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue';
import { Component } from 'vue/types';
import VInput from 'vuetify/es5/components/VInput';

type FileEventTarget = EventTarget & { files: FileList };

export default Vue.extend({
  extends: (VInput as unknown) as typeof Vue,
  props: {
    maxFileSize: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      fileSize: null as null | number,
    };
  },
  computed: {
    hasError(): boolean {
      return (this.fileSize ?? 0) > this.maxFileSize;
    },
  },
  methods: {
    handleFileChange(file: File | undefined): void {
      if (file) {
        this.fileSize = file.size;
      } else {
        this.fileSize = null;
      }
    },
  },
});
</script>
