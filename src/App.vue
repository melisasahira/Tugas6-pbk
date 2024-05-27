<template>
  <div>
    <form @submit.prevent="save">
      <input type="text" v-model="form.title" placeholder="Title" /><br />
      <textarea v-model="form.content" placeholder="Content"></textarea><br />
      <button type="submit">{{ form.id ? 'Update' : 'Save' }}</button>
    </form>
    <ul>
      <li v-for="article in articles" :key="article.id">
        <div class="article">
          <h3>{{ article.title }}</h3>
          <p>{{ article.content }}</p>
          <button @click="edit(article)">Edit</button>
          <button @click="remove(article.id)">Delete</button>
        </div>
      </li>
    </ul>
    <button @click="load">Load</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [],
      form: {
        id: null,
        title: '',
        content: ''
      }
    };
  },
  methods: {
    save() {
      if (this.form.id) {
        // Update existing article
        const index = this.articles.findIndex(article => article.id === this.form.id);
        if (index !== -1) {
          this.articles.splice(index, 1, { ...this.form });
        }
      } else {
        // Add new article
        const newArticle = { ...this.form, id: Date.now().toString() };
        this.articles.push(newArticle);
      }
      this.resetForm();
    },
    edit(article) {
      this.form = { ...article };
    },
    remove(id) {
      const index = this.articles.findIndex(article => article.id === id);
      if (index !== -1) {
        this.articles.splice(index, 1);
      }
    },
    load() {
      // Here we simulate loading data, replace with actual data fetching
      this.articles = [
        { id: '1', title: 'judul ', content: 'Ini Content ' },
        { id: '2', title: 'judul 2', content: 'Ini Content 2' },
        { id: '3', title: 'judul 3', content: 'Ini Content 3' }
      ];
    },
    resetForm() {
      this.form = {
        id: null,
        title: '',
        content: ''
      };
    }
  },
  mounted() {
    this.load(); // Load articles when component is mounted
  }
};
</script>

<style scoped>
/* Gaya untuk artikel */
.article {
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #e09191;
  border-radius: 5px;
}

.article h3 {
  margin-top: 0;
}
</style>