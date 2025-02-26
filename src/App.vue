<script>
//https://opentdb.com/api.php?amount=15&category=21&type=boolean
  export default{
    name: 'App',
    created(){
      this.axios.get('https://opentdb.com/api.php?amount=15&category=21&type=boolean').then((response) => {
        console.log(response.data.results)
      })
    }
  }
</script>

<template>
  <section class="app">
    <div>
      <h2>Texto da pergunta</h2>
    </div>

    <div>
      <input type="radio" name="options" value="True">
      <label>True</label><br>
      <input type="radio" name="options" value="False">
      <label>False</label><br>
    </div>

    <button class="send" type="button">Send</button>
  </section>
</template>

<style scoped>
  .app{
    font-family: Avenir, Arial, Helvetica, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothinig: graysacel;
    text-align: center;
    color: #2c3e50;
    margin: 60px;
    max-width: 960px;
  }
  .app button.send{
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    background-color: #1867c0;
    border: 1 px solid #1867c0;
    cursor: pointer;
  }
</style>
