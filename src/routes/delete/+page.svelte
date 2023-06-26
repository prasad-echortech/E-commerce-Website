<script>
	import Crud from '../crud/+page.svelte';
	import { browser } from '$app/environment';

	let id;
	console.log(id);
	function del() {
		fetch(`http://localhost:3000/products/${id}`, {
			method: 'DELETE'
		}).then((res) => res.json());
		id = '';
	}
</script>

<Crud />
{#if browser}
{#if localStorage.getItem('currentUser') !== null}
<div class="text-center mt-5">
	<h1>Delete Your Products Here</h1>
	<form action="" on:submit|preventDefault={del}>
		<label for="text" class="fs-4">Enter Product Id : </label>
		<input
			type="text"
			bind:value={id}
			class="bg-dark text-white mt-5 p-2 fs-5"
			placeholder="Enter id To Delete"
		/>
		<button class=" btn btn-danger" type="submit">Delete (-)</button>
	</form>
</div>
{/if}
{/if}
