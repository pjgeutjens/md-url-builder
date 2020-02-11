<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset">
      <b-form-textarea
        id="textarea"
        v-model="form.text"
        placeholder="Enter your image URLs..."
        rows="9"
        max-rows="18"
      ></b-form-textarea>
    <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>

    <!-- <pre class="mt-3 mb-0">{{ text }}</pre> -->
  </div>
</template>

<script>
import getUrls from 'get-urls';

export default {
  name: 'Main',
  data() {
      return {
        form: {
          text: ''
        },
        images: []
      }
    },
  methods: {
    onSubmit(evt) {
        let matches = new Set();
        evt.preventDefault()
        matches = getUrls(this.form.text);
        let result = [...matches].filter(item => item.match("/(jpg|png|gif)$/"))
        this.images = result;
      },
    onReset() {
      this.form.text = '';
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} */
</style>
