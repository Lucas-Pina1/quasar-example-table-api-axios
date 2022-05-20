<template>
  <q-page>
  <div class="row">
     <q-table
      dense
      title="Treats"
      :rows="posts"
      :columns="columns"
      separator="cell"
      selection="single"
      v-model:selected="selected"
      row-key="id"
      class="col"
    >

    <template v-slot:body="props">
        <q-tr :props="props">
          <q-td auto-width>
            <q-btn
            size="sm"
            color="accent"
            round
            dense
            @click="props.expand = !props.expand"
            :icon="props.expand ? 'remove' : 'add'"/>
          </q-td>
          <q-td
            v-for="col in props.cols"
            :key="col.name"
            :props="props"
          >
            {{ col.value }}
          </q-td>
        </q-tr>
        <q-tr v-show="props.expand" :props="props">
          <q-td colspan="100%">
            <div class="text-left">{{ props.row.body }}.</div>
          </q-td>
        </q-tr>
      </template>

    <!-- <template v-slot:body-cell-action="props">
        <q-td :props="props">
          <q-btn
          icon="create"
          color="primary"
          size="sm"
          dense
          @click="editPost(props.row.id)"
          />
          <q-btn
          icon="delete"
          color="negative"
          size="sm"
          dense
          class="q-ml-sm"
          @click="deletePost(props.row.id)"
          />
        </q-td>
      </template> -->
     </q-table>
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
        // {
        //   name: 'action',
        //   label: 'Action',
        //   align: 'center',
        //   sortable: true,
        // },
      ],
      posts: [],
      selected: [],
    };
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    getPosts() {
      api.get('/posts').then((res) => {
        this.posts = res.data;
        // console.log(res.data);
      })
        .catch((err) => {
          throw (err);
        });
    },
    editePost(idPost) {
      console.log(idPost);
    },
    deletePost(idPost) {
      console.log(idPost);
    },
  },
};
</script>
