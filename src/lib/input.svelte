<script>
  import { createEventDispatcher } from "svelte";

  export let label = "";
  export let value = "";
  export let error = "";
  export let type = "text";

  const dispatch = createEventDispatcher();

  const handleInput = (event) => {
    value = event.target.value;
    dispatch("input", value);
  };
</script>

<div class="input-group">
  <label>{label}*</label>

  {#if type === "textarea"}
    <textarea bind:value on:input={handleInput}></textarea>
  {:else}
    <input {value} {type} on:input={handleInput} />
  {/if}
  {#if error}
    <span class="error">{error}</span>
  {/if}
</div>

<style>
  .input-group {
    display: flex;
    flex-direction: column;
  }

  label {
    margin-top: 20px;
    font-weight: 300;
    color: #797ea3;
    font-size: 13px;
  }
  input,
  textarea {
    background: none;
    border: none;
    border-bottom: 1px solid #3f4363;
    outline: none;
    color: white;
    padding: 5px 0;
  }

  input:focus,
  textarea:focus {
    border-bottom: 1px solid #ffffff;
  }

  .input-group:focus-within label {
    color: #ffffff;
    transition: 0.3s ease;
  }

  .error {
    font-size: 10px;
    color: rgb(178, 24, 24);
  }
</style>
