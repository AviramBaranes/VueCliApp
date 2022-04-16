<template>
  <base-card>
    <base-button
      :class="storedResourcesBtnClass"
      @click="changeSelectedTab('stored-resource')"
      >Stored Resources</base-button
    >
    <base-button
      :class="addResourceBtnClass"
      @click="changeSelectedTab('add-resource')"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResource from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResource,
    AddResource,
  },
  provide() {
    return {
      resources: this.learningResources,
      createResource: this.createResource,
    };
  },
  computed: {
    storedResourcesBtnClass() {
      return this.selectedTab === 'stored-resource' ? null : 'flat';
    },
    addResourceBtnClass() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  data() {
    return {
      selectedTab: 'stored-resource',
      learningResources: [
        {
          id: '1',
          title: 'google',
          description: 'Learn to google.',
          link: 'https://google.com',
        },
        {
          id: '2',
          title: 'udemy',
          description: 'The best learning resource',
        },
      ],
    };
  },
  methods: {
    changeSelectedTab(tab) {
      this.selectedTab = tab;
    },
    createResource(resource) {
      this.learningResources.unshift(resource);
    },
  },
};
</script>
