<template>
  <q-page>
  <div class="row">
    <q-table
      title="Treats"
      :data="posts"
      :columns="columns"
      row-key="name"
      class="col"
    />
  </div>
  </q-page>
</template>

<script>
import { api } from '../boot/axios';

export default {
  name: 'PageIndex',
  data() {
    return {
      columns: [
        {
          name: 'id',
          field: 'id',
          label: 'Id post',
          align: 'left',
          sortable: true,
        },
        {
          name: 'title',
          field: 'title',
          label: 'Title',
          align: 'left',
          sortable: true,
        },
      ],
      posts: [],
    };
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    getPosts() {
      api.get('/posts').then((res) => {
        this.posts = res.data;
        console.log(res.data);
      })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
