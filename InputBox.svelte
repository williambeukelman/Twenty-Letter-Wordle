<script>
  import { currentRow } from "./stores.js";
  import { keyboard } from "./stores.js";
  import { message } from "./stores.js";
  import { answer } from "./stores.js";

  export let rowNumber;
  let boxes = [
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" },
    { value: "", style: "" }
  ];

  function checkEmpty() {
    for (const [index, letter] of boxes.entries()) {
      if (letter.value === "") {
        return false;
      }
    }
    return true;
  }

  function checkVictory(box) {
    return box.style === "green";
  }

  function evaluateWord() {
    for (const [index, letter] of boxes.entries()) {
      if ($answer[index] === letter.value) {
        boxes[index].style = "green";
        $keyboard[letter.value] = "green";
      } else if (letter.value != "" && $answer.includes(letter.value)) {
        boxes[index].style = "yellow";
        $keyboard[letter.value] = "yellow";
      } else {
        boxes[index].style = "invalid";
        $keyboard[letter.value] = "invalid";
      }
    }
    //Check Victory
    if (boxes.every(checkVictory)) {
      //alert("You won!");
      $message = "You won!";
    } else {
      if ($currentRow >= 5) {
        //alert("You lost!");
        $message = "You lost!";
      }
      //Update row
      currentRow.update(n => n + 1);
    }
  }

  function handleKeys(event) {
    if (event.key === "Backspace" && event.target.previousSibling) {
      event.target.previousSibling.focus();
    } else if (event.key === "Enter") {
      if (checkEmpty()) {
        evaluateWord();
      }
    } else if (event.target.nextSibling && event.target.nextSibling) {
      event.target.nextSibling.focus();
    }
  }
</script>

<style>
  .box {
    width: 4vw;
    text-transform: uppercase;
    text-align: center;
    font-weight: bolder;
    height: 4vw;
    padding: 0;
    max-width: 3rem;
    max-height: 3rem;
    margin: 0.1rem;
    color: darkslategrey;
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

<div class="col d-flex justify-content-center">
	{#each boxes as box, index }
    <input type="text" bind:value="{box.value}"
     class="{box.style} box form-control" 
     id="box{index}" 
     maxlength="1" 
     on:keyup={handleKeys}
     disabled={rowNumber == $currentRow ? false : true}>
	{/each}
</div>

