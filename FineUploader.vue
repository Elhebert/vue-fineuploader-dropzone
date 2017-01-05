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
      const fineUploaderBasicInstance = new qq.FineUploaderBasic({
        ...this.options,
        callbacks: this.callbacks,
      });
      qq.DragAndDrop({
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
