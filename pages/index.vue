<template>
  <div class="container">
    <div class="input">
      <input id="input" v-model="input" name="fName" type="text" :placeholder=this.placeholder>
      <button @click="addItem('pro')">add pro</button>
      <button @click="addItem('con')">add con</button>
    </div>
    <div class="output">
      <div class="pros">
        <legend>pros :</legend>
        <ul v-for="(pro, index) in pros" :key="index">
          <li>{{ pro }} <span @click="deleteItem('pro', index)">X</span></li>
        </ul>
      </div>
      <div class="cons">
        <legend>cons :</legend>
        <ul v-for="(con, index) in cons" :key="index">
          <li>{{ con }} <span @click="deleteItem('con', index)">X</span></li>
        </ul>
      </div>
    </div>
    <div id="controls">
      <button @click="clear">Clear Board</button>
      <button @click="saveBoard">save board as : </button><input v-model="boardName" type="text">
    </div>
    <ul v-for="board in boards" :key="board">
      <li class="boards-list"><nuxt-link class="nuxt-link" :to="`/boards/${board.id}`">{{ board.name }}</nuxt-link></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      input: '',
      pros: [],
      cons: [],
      boardName: '',
      boardId: '1',
      boards: JSON.parse(localStorage.getItem('boards')),
      placeholder: 'enter text here !'
    }
  },

  methods: {

    saveBoard() {
      const boards = JSON.parse(localStorage.getItem('boards')) || [];
      const newBoard = {
        id: boards.length + 1,
        name: this.boardName,
        pros: [...this.pros],
        cons: [...this.cons]
      }
      if (!this.pros.length && !this.cons.length) {
        alert('you cant save an empty board')
        return
      } else if (!this.boardName) {
        alert('you must choose a name to save the board ...')
        return
      }
      else {
        boards.push(newBoard)
        localStorage.setItem('boards', JSON.stringify(boards))
        this.boardName = ''
      }
      window.location.reload();
    },




    addItem(type) {
      let item = this.input.trim();

      if (item === '') {
        this.placeholder = 'You must enter some text..';
      } else if (this.pros.includes(item)
        || this.cons.includes(item)) {
        this.placeholder = 'This item is already listed!';
        this.input = ''
      } else {
        if (type === 'pro') {
          this.pros.push(item);
          this.input = '';
          this.placeholder = 'enter your text here';
        }
        if (type === 'con') {
          this.cons.push(item);
          this.input = '';
          this.placeholder = 'enter your text here';
        }
      }
    },
    deleteItem(type, index) {
      if (type === 'pro') {
        this.pros.splice(index, 1);
      } else if (type === 'con') {
        this.cons.splice(index, 1);
      }
    },
    clear() {
      this.input = '',
        this.cons = [],
        this.pros = []
    }
  }
}

</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Gloria+Hallelujah&family=Orbitron:wght@400..900&display=swap');

#controls {
  display: flex;
  flex-direction: row;
  width: 850px;
}

.boards-list {
  font-family: "Gloria Hallelujah", cursive;
  font-size: 34px;
  cursor: pointer;
}

.nuxt-link {
  text-decoration: none;
  color: rgb(255, 255, 255);
}

.nuxt-link:visited {
  text-decoration: none;
  color: white
}

.boards-list:hover {
  border-radius: 5%;
  padding: 5px;
  box-shadow: rgba(0, 0, 0, 0.17) 0px -23px 25px 0px inset, rgba(0, 0, 0, 0.15) 0px -36px 30px 0px inset, rgba(0, 0, 0, 0.1) 0px -79px 40px 0px inset, rgba(0, 0, 0, 0.06) 0px 2px 1px, rgba(0, 0, 0, 0.09) 0px 4px 2px, rgba(0, 0, 0, 0.09) 0px 8px 4px, rgba(0, 0, 0, 0.09) 0px 16px 8px, rgba(0, 0, 0, 0.09) 0px 32px 16px;
}

.gloria-hallelujah-regular {
  font-family: "Gloria Hallelujah", cursive;
  font-weight: 300;
  font-style: normal;
}

html {
  margin: 0;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  box-shadow: 0px 0px 6px 5px rgba(58, 18, 13, 0), 0px 0px 0px 2px #c2a782, 0px 0px 0px 4px #a58e6f, 3px 4px 8px 5px rgba(0, 0, 0, 0.5);
  background-image: radial-gradient(circle at left 30%, rgba(34, 34, 34, 0.3), rgba(34, 34, 34, 0.3) 80px, rgba(34, 34, 34, 0.5) 100px, rgba(51, 51, 51, 0.5) 160px, rgba(51, 51, 51, 0.5)), linear-gradient(215deg, transparent, transparent 100px, #222 260px, #222 320px, transparent), radial-gradient(circle at right, #111, rgba(51, 51, 51, 1));
  background-color: #333;
  color: whitesmoke;
}

.container {
  padding: 1rem;
  display: grid;
  place-items: center;
}

.input {
  min-width: 400px;
  width: 820px;
  width: 45%;
  margin: auto;
}

input {
  width: 92%;
  height: 40px;
  font-family: "Gloria Hallelujah", cursive;
  background-color: #333;
  color: whitesmoke;
  padding-left: 12px;
  border: solid white;
  border-width: 3px 3px 5px 5px;
  border-radius: 4% 95% 6% 95%/95% 4% 92% 5%;
}

input:focus {
  outline: none;
}

button {
  width: 45.5%;
  height: 40px;
  font-family: "Gloria Hallelujah", cursive;
  font-size: larger;
  background-color: #333;
  color: whitesmoke;
  border: none;
  margin: 5px;
}

.output {
  display: flex;
  flex-direction: row;
  min-width: 400px;
  width: 870px;
  font-size: 1.6rem;
  font-family: "Gloria Hallelujah", cursive;
}

.pros,
.cons {
  width: 45%;
  min-height: 300px;
  border: solid white;
  border-width: 3px 3px 5px 5px;
  border-radius: 4% 95% 6% 95%/95% 4% 92% 5%;
  transform: rotate(-2deg);
  padding-left: 12px;
}

span {
  float: right;
  margin-right: 13px;
}

::marker {
  content: '* ';
  color: white;
}
</style>
