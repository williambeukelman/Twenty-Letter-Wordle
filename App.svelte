<script>
  import Button from "./Button.svelte";
  import InputBox from "./InputBox.svelte";
  import Keyboard from "./Keyboard.svelte";
  import Info from "./Info.svelte";
  import { wordList } from "./stores.js";

  let rows = Array(5).fill("");
  let givenWord = "";

  function giveWord() {
    let random = Math.floor(Math.random() * $wordList.length);
    givenWord = $wordList[random];
  }
</script>

<style>
  main {
    font-family: sans-serif;
    text-align: center;
  }
  h1,
  h3 {
    text-transform: uppercase;
    color: darkslategrey;
  }
</style>

<main>
	<h1>Wordle (HARDMODE)</h1>
  <div class="container">
  	{#each rows as row, i}
      <div class="row mb-1">
        <InputBox rowNumber={i}/>
      </div>
  	{/each}
  </div>
  <div class="container d-flex justify-content-center mt-4">
    <Keyboard/>
  </div>
  <div class="container d-flex justify-content-center mt-4">
    <div class="row">
      <Info/>
    </div>
    <div class="row d-flex justify-content-center">
      <div class="col-5 mt-5 mb-2">
        <p>Guess a word by typing above. Grey the letter isn't in the word, yellow: wrong place, green: you got it.</p>
        <button on:click={giveWord} class="btn btn-outline-danger">I don't known any 20 letter words!</button>
      </div>
      <div class="col-12 justify-content-center">
        {#if givenWord != ""}
          <h3>{givenWord}</h3>
        {/if}
      </div>
    </div>
  </div>
</main>
