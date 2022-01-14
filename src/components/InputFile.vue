<template lang="">
  <div class="inputfile fx-col">
      <input
        ref="inputFile"
        type="file"
        @change="changeFile($event)"
        class="inputfile__main"
      />
  </div>
</template>
<script>
export default {
  name: "InputFile",
  props: {
    value: {
      type: [String, Event],
      default: null,
    },
  },
  data() {
    return {
      files: [],
      reader: new FileReader(),
    };
  },
  methods: {
    changeFile(e) {
      this.files = e.target.files;
      this.fileName = this.files[0].name;
      // Convert sang bytearray và truyền ra
      this.reader = new FileReader();
      this.reader.onload = () => {
        this.readerImage();
      };
      this.reader.readAsArrayBuffer(this.files[0]);
    },
    /**
     * Chuyển sang mảng ký tự
     * CreatedBy: NTDUNG (19/12/2021)
     */
    readerImage() {
      // var binaryString2 = btoa(String.fromCharCode(...(new Uint8Array(this.reader.result))))
      var binaryString = [],
        bytes = new Uint8Array(this.reader.result),
        length = bytes.length;
      for (var i = 0; i < length; i++) {
        binaryString[i] = String.fromCharCode(bytes[i]);
      }
      var data = btoa(binaryString.join(""));
      this.$emit("input", data);
    },
  },
};
</script>
<style lang="scss">
</style>
