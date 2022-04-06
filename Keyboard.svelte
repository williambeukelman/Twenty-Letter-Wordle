<script>
  import { keyboard } from "./stores.js";

  function handleClick(event) {
    /*
                          if (event.key === "Backspace") {
                            event.target.previousSibling.focus();
                          } else if (event.target.nextSibling) {
                            event.target.nextSibling.focus();
                          }
                          */
  }
</script>

<style>
  .key {
    color: darkslategrey;
    background-color: #dce1ed;
    width: 3rem;
    height: 3rem;
    text-transform: uppercase;
    text-align: center;
    font-weight: bolder;
  }
  .green,
  .yellow,
  .invalid {
    color: white;
  }
  .green {
    background-color: #79b851;
  }
  .yellow {
    background-color: #f3c237;
  }
  .invalid {
    background-color: #a4aec4;
  }
</style>

<div class="col-12 col-md-8 d-flex flex-wrap justify-content-center">
	{#each Object.entries($keyboard) as letter, i}
    <button class="{letter[1]} key btn btn-light" id="box" on:click={handleClick}>{letter[0]}</button>
	{/each}
</div>
