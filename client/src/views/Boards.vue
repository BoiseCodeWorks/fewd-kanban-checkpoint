<template>
  <div class="boards container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center">WELCOME TO THE BOARDS!!!</h1>
      </div>
    </div>
    <div class="row">
      <div class="card col-3 align-items-center justify-content-center" v-for="board in boards" :key="board._id">
        <router-link :to="{name: 'board', params: {boardId: board._id}}"><h2>{{board.title}}</h2></router-link>
        <button @click="deleteBoard(board._id)">DELETE BOARD</button>
      </div>
      <form class="card col-3" @submit.prevent="addBoard">
        <input type="text" placeholder="title" v-model="newBoard.title" required>
        <input type="text" placeholder="description" v-model="newBoard.description">
        <button type="submit">Create Board</button>
      </form>
    </div>
  </div>
</template>

<script>
  export default {
    name: "boards",
    created() {
      //blocks users not logged in
      if (!this.$store.state.user._id) {
        this.$router.push({ name: "login" });
      }
    },
    mounted() {
      this.$store.dispatch("getBoards");
    },
    data() {
      return {
        newBoard: {
          title: "",
          description: ""
        }
      };
    },
    computed: {
      boards() {
        return this.$store.state.boards;
      }
    },
    methods: {
      addBoard() {
        this.$store.dispatch("addBoard", this.newBoard);
        this.newBoard = { title: "", description: "" };
      },
      deleteBoard(boardId) {
        let confirmDelete = confirm("Are you sure you want to delete this board?\nAll of the information will be lost.")
        if(!confirmDelete) return
        this.$store.dispatch("deleteBoard", boardId);
      }
    }
  };
</script>