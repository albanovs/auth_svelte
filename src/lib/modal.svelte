<script>
  export let message = "";
  export let show = false;
  export let onClose = () => {};

  let timeoutId;

  $: if (show) {
    if (timeoutId) {
      clearTimeout(timeoutId);
    }
    timeoutId = setTimeout(() => {
      onClose();
    }, 3000);
  } else {
    if (timeoutId) {
      clearTimeout(timeoutId);
    }
  }

  const closeModal = () => {
    onClose();
  };
</script>

{#if show}
  <div class="modal-overlay" on:click={closeModal}>
    <div class="modal-content" on:click|stopPropagation>
      <p>{message}</p>
      <button on:click={closeModal}>Close</button>
    </div>
  </div>
{/if}

<style>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .modal-content {
    background: white;
    border-radius: 8px;
    padding: 20px;
    max-width: 500px;
    width: 100%;
    text-align: center;
    animation: fadeIn 0.3s;
    color: green;
  }

  button {
    margin-top: 10px;
    padding: 10px 20px;
    border: none;
    background-color: #2c2f47;
    color: white;
    cursor: pointer;
    border-radius: 4px;
  }

  button:hover {
    background-color: #1a1d2a;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>
