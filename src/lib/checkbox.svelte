<script>
  import { createEventDispatcher } from "svelte";

  export let label = "";
  export let checked = false;
  export let error = "";

  const dispatch = createEventDispatcher();

  const handleChange = (event) => {
    checked = event.target.checked;
    dispatch("change", checked);
  };
</script>

<div class="custom-checkbox">
  <label>
    <input type="checkbox" bind:checked on:change={handleChange} />
    <span class="checkbox-custom"></span>
  </label>
  {#if error}
    <span class="error">{error}</span>
  {/if}
</div>

<style>
  input[type="checkbox"] {
    position: absolute;
    opacity: 0;
    cursor: pointer;
  }

  .custom-checkbox {
    display: flex;
    align-items: center;
    font-size: 16px;
    font-family: sans-serif;
    cursor: pointer;
    user-select: none;
  }

  .checkbox-custom {
    width: 20px;
    height: 20px;
    background-color: none;
    border: 2px solid #3f4363;
    border-radius: 8px;
    margin-right: 10px;
    display: inline-block;
    position: relative;
    transition:
      background-color 0.3s,
      border-color 0.3s;
  }

  .checkbox-custom::after {
    content: "";
    background: url(../img/check.svg) no-repeat center center;
    background-size: cover;
    width: 16px;
    height: 16px;
    position: absolute;
    display: none;
    left: 3.5px;
    top: 4px;
  }

  input[type="checkbox"]:checked + .checkbox-custom {
    background-color: #2c2f47;
    border: none;
    width: 23.2px;
    height: 23.2px;
  }

  input[type="checkbox"]:checked + .checkbox-custom::after {
    display: block;
  }

  input[type="checkbox"]:hover + .checkbox-custom {
    border-color: #8f94b8cc;
  }
</style>
