<template>
  <tr>
    <td>{{ item.name }}</td>
    <td>{{ item.deadline }}</td>
    <th>
      <button @click="testIndex()" class="btn btn-warning">Edit</button>
      <button
        @click="testIndex2()"
        class="btn btn-warning"
        style="background-color: red"
      >
        Delete
      </button>
    </th>
  </tr>
</template>

<script>
export default {
  name: "ItemsComponent",
  
  props: ['item'],

  methods: {
    
    testIndex(index) {
      this.$emit('msg-index',index)
    },
    testIndex2(index) {
      this.$emit('msg-index2',index)
    }
  },
  
};
</script>