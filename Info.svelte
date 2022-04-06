<script>
  import { message } from "./stores.js";
  function resetGame() {
    location.reload();
    return false;
  }
</script>

<style>
</style>

<div class="col-12 col-md-8 d-flex flex-wrap justify-content-center">
  {#if $message != ""}
  <button class="btn btn-success" on:click={resetGame}>{ $message } Play Again?</button>
  {/if}
</div>