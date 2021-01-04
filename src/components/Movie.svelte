<script>
  import store from '../store'
  export let movie

  const setMovie = () => {
    store.update(state => ({
      ...state,
      ...movie
    }))
  }
</script>

<div class="movie">
  <figure
    on:click={setMovie}
    class:selected="{movie.id === $store.id}"
    class:not-selected="{movie.id === $store.id}">
    <img src={movie.url} alt={movie.title}>
  </figure>
</div>

<style>
  .movie {
    padding: 0;
    margin: 0;
  }
  .selected img {
    transition: height .7s ease;
    height: 170px;
    border: 2px solid var(--color);
  }
  .not-selected img {
    transition: height .7s ease-out;
  }
  figure {
    padding: 0;
    margin: 0;
    margin-right: .5rem;
    cursor: pointer;
  }
  img {
    height: 150px;
    width: 116px;
    object-fit: cover;
    border-radius: .5rem;
    overflow: hidden;
    border: 2px solid transparent;
  }
  @keyframes height {

  }
</style>