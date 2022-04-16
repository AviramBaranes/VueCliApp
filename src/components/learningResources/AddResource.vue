<template>
  <base-dialog v-if="!isFieldsValid"> </base-dialog>
  <base-card>
    <form @submit.prevent="submitHandler">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" ref="inputTitle" />
      </div>
      <div>
        <label for="description">Description</label>
        <textarea
          rows="3"
          name="description"
          id="description"
          ref="inputDescription"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" name="link" id="link" ref="inputLink" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['createResource'],
  data() {
    return {
      isFieldsValid: true,
    };
  },
  methods: {
    submitHandler() {
      const title = this.$refs.inputTitle.value;
      const description = this.$refs.inputDescription.value;
      const link = this.$refs.inputLink.value;

      if (
        !this.isValid(title) ||
        !this.isValid(description) ||
        !this.isValid(link)
      ) {
        this.isFieldsValid = false;
        return;
      }

      this.createResource({ title, description, link });
    },
    isValid(value) {
      return value.trim() !== '';
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
