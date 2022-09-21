<template>
  <div class="blocks-list">
    <h3>Название блока:</h3>
    <input type="text" v-model="newBlockName" />
    <button @click="addBlockName(newBlockName)">Добавить</button>
    <ul class="blocks">
      <li v-for="blocks in this.blocksList">
        <a href="#">{{ blocks.name }}</a>
        <button class="deleteBlockNameBtn" @click="deleteBlockName(blocks.id)">
          <img src="../assets/delete.svg" width="18" height="18" alt="" />
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'blocksList',
  data() {
    return {
      url: 'https://63298cf64c626ff832c3e401.mockapi.io/library',
      newBlockName: '',
      blocksList: '',
    };
  },
  methods: {
    getBlocksList() {
      fetch(this.url)
        .then((response) => response.json())
        .then((data) => (this.blocksList = data));
    },
    addBlockName(name) {
      const newData = {
        name: name,
        words: [],
      };
      if (name.length > 0) {
        fetch(this.url, {
          method: 'POST',
          body: JSON.stringify(newData),
          headers: {
            'Content-Type': 'application/json',
          },
        });
        this.blocksList = [...this.blocksList, newData];
      } else {
        alert('empty');
      }
    },
    deleteBlockName(id) {
      fetch(this.url + `/${id}`, {
        method: 'DELETE',
      });
      this.blocksList.forEach((el, i) => {
        if (el.id == id) this.blocksList.splice(i, 1);
      });
    },
  },
  created() {
    this.getBlocksList();
  },
};
</script>

<style lang="scss" scoped>
.blocks {
  margin-top: 20px;
}

.deleteBlockNameBtn {
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
</style>
