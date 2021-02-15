<template>
  <div id="app">
    <Header />
    <main>
      <Navigation
        :navItems="technologyNames"
        @nav-click="onMenuClick"
        @on-create-subject="onCreateSubject"
      />
      <div class="main-content">
        <Subjects
          :technologies="tutorials.technologies"
          :selectedMenuId="selectedMenuId"
          :selectedSubject="selectedSubject"
          @subject-click="onSubjectClick"
        />
        <Content :technologies="technologyNames">
          <NewSubject
            v-if="isCreateView"
            :technologies="technologyNames"
            @on-save="onSubjectSave"
          />
          <div v-else v-html="selectedContent"></div>
        </Content>
      </div>
    </main>

    <Footer />
  </div>
</template>

<script>
import Header from "@/components/core/Header.vue";
import Footer from "@/components/core/Footer.vue";
import Subjects from "@/components/core/Subjects.vue";
import Navigation from "@/components/core/Navigation.vue";
import Content from "@/components/core/Content.vue";
import NewSubject from "@/components/NewSubject.vue";

import jsonData from "./assets/tutorials.json";

const defaultMenuId = jsonData.technologies[0].id;

export default {
  name: "App",
  components: {
    Header,
    Footer,
    Subjects,
    Content,
    Navigation,
    NewSubject,
  },
  data() {
    return {
      isCreateView: false,
      tutorials: { ...jsonData },
      selectedMenuId: defaultMenuId,
      selectedSubject: "",
    };
  },
  computed: {
    technologyNames() {
      return this.tutorials.technologies.map((tech) => ({
        id: tech.id,
        name: tech.name,
      }));
    },
    selectedContent() {
      const { subjects } = this.tutorials.technologies.find(
        (tech) => tech.id === this.selectedMenuId
      );
      const subject = subjects.find((sub) => sub.name === this.selectedSubject);
      return subject ? subject.content : "";
    },
  },
  methods: {
    onMenuClick(id) {
      this.selectedMenuId = id;
      this.selectedSubject = "";
      this.isCreateView = false;
    },
    onSubjectClick(name) {
      this.selectedSubject = name;
      this.isCreateView = false;
    },
    onCreateSubject() {
      this.isCreateView = true;
      this.selectedSubject = "";
    },
    onSubjectSave(technologyId, newData) {
      const { technologies } = this.tutorials;
      const selectedTech = technologies.find(
        (tech) => tech.id === technologyId
      );
      selectedTech.subjects.push(newData);
      this.isCreateView = false;
    },
  },
};
</script>

<style></style>
