<template>
  <div>
    <div class="form-group">
      <input placeholder="Technology subject..." type="text" id="subject" />
    </div>

    <vue-editor v-model="content" />

    <select name="technologies" id="technologies">
      <option value="default" selected>Select a technology...</option>
      <option value="c-sharp">C#</option>
      <option value="java">JAVA</option>
      <option value="javscript">JAVASCRIPT</option>
      <option value="python">PYTHON</option>
    </select>
    <button class="btn">Create</button>
    <h3>Content preview</h3>
    <div class="content-preview" v-html="content"></div>
  </div>
</template>

<script>
import { VueEditor } from "vue2-editor";
export default {
  components: {
    VueEditor,
  },
  data() {
    return {
      content: "",
    };
  },
};
</script>

<style></style>
