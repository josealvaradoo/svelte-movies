<script>
	import { onMount } from 'svelte'
	import store from './store'
	import Snackbar from './components/Snackbar.svelte'
	import Loader from './components/Loader.svelte'
	import Page from './components/Page.svelte'
	import Thumbnail from './components/Thumbnail.svelte'

	let data = []
	const API_KEY = 'f3abb031'
	const query = 'avengers'

	const getMovies = async () => {
		try {
			const protocol = 'https'
			const response = await fetch(`${protocol}://omdbapi.com/?s=${query}&apikey=${API_KEY}&plot=full`)
			const dataJSON = await response.json()
			
			const fetchData = [...Array.from(dataJSON.Search).reduce((arr, item) => {
				const movie = {
					id: item.imdbID,
					url: item.Poster.replace('X300', ''),
					title: item.Title
				}

				return arr.concat(movie)
			}, [])]

			data = fetchData

			const first = data[0]
			
			store.update(state => ({
				...state,
				...first
			}))
		} catch(error) {
			store.update(state => ({
				...state,
				show: true,
				type: 'error',
				title: error.message
			}))
		}
	}

	onMount(() => {
		getMovies()
	})
</script>

<main>
	<Snackbar />
	{#if (data.length > 0)}
		<Page />
	{:else}
	<Loader />
	{/if}
	<Thumbnail {data} />
</main>

<style>
	:global(:root) {
		--primary: #3e2723;
		--light-primary: #d3b8ae;
		--dark-primary: #1b0000;
		--secondary: #bb4d00;
		--dark-secondary: #ac1900;
		--success: #558b2f;
		--error: #c62828;
		--white: #fff;
		--color: #ffc107;
		--font-family: 'Orbitron', sans-serif;
	}
	main {
		padding: 0;
		margin: 0;
		height: 100%;
	}
</style>