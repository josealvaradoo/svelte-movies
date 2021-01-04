<script>
  import Movie from './Movie.svelte'
  export let data
</script>

<div class="thumbnail">
  <div class="thumbnail-movies">
    {#each data as movie (movie.id)}
      <Movie {movie} />
    {/each}
  </div>
</div>

<style>
  .thumbnail {
    color: var(--white);
    position: absolute;
    z-index: 1;
    bottom: 0;
  }
  .thumbnail-movies {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    overflow-x: auto;
    max-width: 100vw;
    align-items: flex-end;
  }
</style>