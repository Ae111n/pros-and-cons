<template>
     <div id="outer-div">
          <button id="home-button"><nuxt-link class="nuxt-link" :to="`/`">go back to home page</nuxt-link></button>
          <h1>{{ board.name }} , ID : {{ board.id }}</h1>
          <div class="container2">

               <div class="pros">
                    <legend>pros :</legend>
                    <ul v-for="pro in board.pros" :key="pro">
                         <li>{{ pro }}</li>
                    </ul>
               </div>

               <div class="cons">
                    <legend>cons :</legend>
                    <ul v-for="con in board.cons" :key="con">
                         <li>{{ con }}</li>
                    </ul>
               </div>
          </div>

          <div id="boards-list">
               <ul v-for="board in boards" :key="board">
                    <legend>boards list : </legend>

                    <li class="boards-list">
                         <nuxt-link class="nuxt-link" :to="`/boards/${board.id}`">
                              {{ board.name }}
                         </nuxt-link>
                    </li>

               </ul>
          </div>

     </div>
</template>

<script>

export default {
     data() {
          return {
               board: {},
          }
     },
     mounted() {
          const boards = JSON.parse(localStorage.getItem('boards')) || [];
          const boardId = this.$route.params.id;
          this.board = boards.find(b => b.id === parseInt(boardId));
          this.boards = boards
     }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Gloria+Hallelujah&family=Orbitron:wght@400..900&display=swap');

html {
     margin: 0;
     width: 100%;
     height: 100%;
     box-sizing: border-box;
     box-shadow: 0px 0px 6px 5px rgba(58, 18, 13, 0), 0px 0px 0px 2px #c2a782, 0px 0px 0px 4px #a58e6f, 3px 4px 8px 5px rgba(0, 0, 0, 0.5);
     background-image: radial-gradient(rgba(34, 34, 34, 0.3), rgba(34, 34, 34, 0.3) 80px, rgba(34, 34, 34, 0.5) 100px, rgba(51, 51, 51, 0.5) 160px, rgba(51, 51, 51, 0.5)), linear-gradient(215deg, transparent, transparent 100px, #222 260px, #222 320px, transparent), radial-gradient(#111, rgba(51, 51, 51, 1));
     background-color: #333;
     color: whitesmoke;
     font-family: "Gloria Hallelujah", cursive;
     display: grid;
     place-items: center;
}

::marker {
     content: '* ';
     color: white;
}

.container2 {
     display: flex;
     width: 1200px;
     height: auto;
}

.pros,
.cons {
     width: 50%;
     min-height: 300px;
     border: solid white;
     border-width: 3px 3px 5px 5px;
     border-radius: 4% 95% 6% 95%/95% 4% 92% 5%;
     transform: rotate(-2deg);
     padding-left: 12px;
     font-size: 28px;
}

legend {
     font-size: 30px;
     position: inherit;
}

h1 {
     width: 100%;
     text-align: center;
}

.boards-list {
     font-family: "Gloria Hallelujah", cursive;
     font-size: 34px;
     width: fit-content;
}

#boards-list {
     width: fit-content;
}

.boards-list:hover {
     border-radius: 5%;
     padding: 5px;
     box-shadow: rgba(0, 0, 0, 0.17) 0px -23px 25px 0px inset, rgba(0, 0, 0, 0.15) 0px -36px 30px 0px inset, rgba(0, 0, 0, 0.1) 0px -79px 40px 0px inset, rgba(0, 0, 0, 0.06) 0px 2px 1px, rgba(0, 0, 0, 0.09) 0px 4px 2px, rgba(0, 0, 0, 0.09) 0px 8px 4px, rgba(0, 0, 0, 0.09) 0px 16px 8px, rgba(0, 0, 0, 0.09) 0px 32px 16px;
}

.nuxt-link {
     text-decoration: none;
     color: rgb(255, 255, 255);
}

.nuxt-link:visited {
     text-decoration: none;
     color: white
}

#home-button {
     width: 240px;
}
</style>