<script>
  export default {
    name: "App",
    data() {
      return {
        clickedSquares: [],
      };
    },
    methods: {
      getChessNotation(index) {
        const columns = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'];
        const row = 8 - Math.floor((index - 1) / 8);
        const column = columns[(index - 1) % 8];
        return `${column}${row}`;
      },
      logSquare(index) {
        this.clickedSquares.push(this.getChessNotation(index));
        this.scrollToBottom();
      },
      scrollToBottom() {
        this.$nextTick(() => {
          const sidebar = this.$el.querySelector('.sidebar');
          sidebar.scrollTop = sidebar.scrollHeight;
        });
      }
    },
  };
</script>

<template>
  <div id="app">
    <main class="main-container">
      <div class="chessboard">
        <div
          v-for = "index in 64"
          :key = "index"
          :class="[
            'square', 
            (Math.floor((index - 1) / 8) + index) % 2 === 0 ? 'dark' : 'light', 
          ]"
          @click="logSquare(index)"
        > 
        </div>
      </div>
    
      <div class="sidebar-container">
        <h2>Clicked Squares</h2>
          <aside class="sidebar">
            <ol>
              <li v-for="(square, idx) in clickedSquares" :key="idx">{{ square }}</li>
            </ol>
          </aside>
      </div>
    </main>
  </div>
</template>

<style>
  #app {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .main-container {
    display: flex;
    flex: 1;
    width: 100%;
    height: 100%;
    justify-content: space-between;
    align-items: center;
  } 

  .sidebar {
    width: 16rem; 
    height: 50vh;
    border-left: 2px solid #ccc;  
    padding: 1rem;
    margin-left: 13vh;
    overflow-y: auto;
  }

  .sidebar-container h2 {
    padding-left: 20vh;
    padding-bottom: 1rem;
    text-align: center; 
  }

  .chessboard {
    display: grid;
    grid-template-columns: repeat(8, 1fr);
    grid-template-rows: repeat(8, 1fr);
    flex: 1;
    margin-top: 5vh;
    height: 80vh;
    border: 0.2rem solid black;
    overflow:visible;
  }

  .square {
    aspect-ratio: 1;
    cursor: pointer;
    position: relative;
  }

  .light {
    background-color: #ffffff;
  } 

  .dark {
    background-color: #000000;
  }

  .square:active {
    outline: 3px solid #ffcc00;
    box-shadow: 0 0 10px 3px #ffcc00;
    z-index: 1;
  }

  @media (max-width: 900px) {
    .main-container {
      flex-direction: column; 
      align-items: center;
      flex: 1;
    }

    .chessboard {
      max-width: 90vw; 
      width: 70%;
      aspect-ratio: 1; 
    }

    .sidebar {
      max-width: none;
      margin-left: 0;
      border-left: none;  
      border-top: 2px solid #ccc;
    }
    
    .sidebar-container {
      /* display: flex;
      flex: auto;
      flex-direction: column;
      align-items: center; */
      margin-top: 2rem;
      flex: 1;
    }

    .sidebar-container h2 {
      margin-top: 2vh;
      padding-left: 0;
      padding-bottom: 0;
    }
  }
</style>
