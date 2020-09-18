<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p :id="idtest">{{ test }} {{ testcomputed }} </p>
    <p v-for="(pizza, index) in pizzas" v-bind:key="index">
      {{ index }} : {{ pizza }}
    </p>
    <!-- <input type="file" v-model="file" /> -->
    <input
      multiple="multiple"
      autocomplete="off"
      type="file"
      @change="onFiles($event)"
      class="form-control"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
interface FileI extends Blob {
  lastModified: number;
  lastModifiedDate: Date;
  name: string;
  size: number;
  type: string;
  webkitRelativePath: string;
  // slice: Slice;
}
export default Vue.extend({
  data() {
    return {
      test: "asdf",
      idtest:"pizza",
      pizzas: ["pepperoni", "cheese"],
      file: {} as any,
      // 5 mb maxsize
      maxAllowedSize: 5 * 1024 * 1024,

      files: [] as any[]
    };
  },
  computed:{
    testcomputed: function(){
      return "blank";
    }
  },
  methods: {
    onFiles(e: any) {
      const files: FileI[] = e.target.files || e.dataTransfer.files;
      if (!files.length || files[0].size > this.maxAllowedSize) return;
      console.log(files);
      // reset journal attachments
      // use vue $set
      this.test = "asdf12";

      for (let i = 0; i < files.length; i++) {
        console.log(files[i]);
        this.createUploadFile(files[i]);
      }
    },
    createUploadFile(file: FileI) {
      const reader = new FileReader();
      reader.onload = e => {
        if (e.target && e.target.result) {
          console.log("attachment parsed");
          console.log(e);
          console.log(file);

          // add to attachments
          const attachment: any = {
            filename: file.name,
            base64: e.target.result.toString(),
            size: file.size,
            mime: file.type
          };
          this.files.push(attachment);
        }
      };
      reader.readAsDataURL(file);
    }
  }
});
</script>
