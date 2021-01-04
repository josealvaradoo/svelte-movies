<script>
  import store from '../store'

  const trailer = () => {
    store.update(state => ({
      ...state
    }))
  }
</script>

<div class="cover">
  <div class="background" style="background:url({$store.url}) no-repeat;">
    <div class="cover-container">
      <div class="trailer" on:click={trailer}>
        <i class="fab fa-youtube"></i>
        <span>Ver trailer</span>
      </div>
      <div class="title">
        {$store.title}
      </div>
    </div>
  </div>
</div>

<style>
  .cover {
    height: 100vh;
    user-select: none;
  }
  .background {
    height: 100%;
    background-position: center;
  }
  .background::after {
    content: "";
    position: fixed;
    background: var(--dark-primary);
    filter: opacity(.65);
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }
  .cover-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    height: 100%;
    position: relative;
    z-index: 1;
    color: var(--color);
    font-family: var(--font-family);
  }
  .title {
    font-weight: 900;
    font-size: 2.5rem;
  }
</style>