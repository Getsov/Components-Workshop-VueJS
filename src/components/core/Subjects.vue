<template>
  <aside class="content-navigation">
    <ul>
      <li
        v-for="(subject, index) in subjects"
        :key="index"
        :class="{ active: isActive(subject.name) }"
        @click="onSubjectClick(subject.name)"
      >
        <a href="#"> {{ subject.name }}</a>
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  props: {
    technologies: {
      type: Array,
      required: true,
    },
    selectedMenuId: {
      type: String,
      required: true,
    },
    selectedSubject: {
      type: String,
      required: true,
    },
  },
  computed: {
    subjects() {
      const { subjects } = this.technologies.find(
        (tech) => tech.id === this.selectedMenuId
      );
      return subjects;
    },
  },
  methods: {
    onSubjectClick(name) {
      this.$emit("subject-click", name);
    },
    isActive(subjectName) {
      return this.selectedSubject === subjectName;
    },
  },
};
</script>

<style></style>
