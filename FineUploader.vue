<template>
  <div>
    <slot></slot>
  </div>
</template>

<style lang="scss">
</style>

<script language="text/babel">
  import qq from 'fine-uploader/lib/all';

  export default {
    props: {
      button: {
        type: String,
      },
      options: {
        type: Object,
        default: () => Object(),
      },
      callbacks: {
        type: Object,
        default: () => Object(),
      },
      dropZone: {
        type: Object,
        default: () => Object(),
      },
    },

    mounted() {
      /* eslint-disable */

      const fineUploaderBasicInstance = new qq.FineUploaderBasic({
        button: window.document.querySelector(this.button),
        ...this.options,
        callbacks: this.callbacks,
      });

      new qq.DragAndDrop({
        dropZoneElements: window.document.querySelectorAll(this.dropZone.element),
        classes: {
          dropActive: this.dropZone.dropActive,
        },
        callbacks: {
          processingDroppedFilesComplete: (files) => {
            fineUploaderBasicInstance.addFiles(files);
          },
        },
      });
    },
  };
</script>
