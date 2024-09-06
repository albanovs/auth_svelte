<script>
  export let color = "blue";
  export let onClick = () => {};
</script>

<button
  class="submit-button"
  style="background-color: {color}"
  on:click={onClick}
>
  Send
</button>

<style>
  .submit-button {
    padding: 10px 40px;
    border: none;
    color: white;
    cursor: pointer;
    font-size: 1rem;
    border-radius: 50px;
  }
  .submit-button:hover {
    opacity: 0.8;
  }
</style>
