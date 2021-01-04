<script>
  import store from '../store'
  import { fade } from 'svelte/transition'

  const close = () => {
    store.update(state => ({
      ...state,
      show: null,
      type: null,
      title: null
    }))
  }
</script>

<div>
  { #if $store.show }
  <div class="snackbar" transition:fade on:click={ close }>
    <div class={`${ $store.type } snackbar-container`}>
      <span>{ $store.title }</span>
      <i class="fas fa-times close"></i>
    </div>
  </div>
  { /if }
</div>

<style>
  .snackbar {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 10;
    font-family: var(--font-family);
  }
  .snackbar-container {
    display: flex;
    flex-direction: row;
    padding: 1rem;
    color: var(--white);
  }
  .success {
    background-color: var(--success);
  }
  .error {
    background-color: var(--error);
  }
  .close {
    position: absolute;
    top: 0;
    right: 0;
    margin: 1rem;
    color: var(--white);
  }
</style>