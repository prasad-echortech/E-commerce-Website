<script>
	import { goto } from '$app/navigation';
	// import { get } from 'svelte/store';
	import Navprod from '../navproducts/+page.svelte';
	function ProAdd() {
		if (localStorage.getItem('currentUser') !== null) {
			goto('/add');
		}
	}
	function ProUp() {
		if (localStorage.getItem('currentUser') !== null) {
			goto('/delete');
		}
	}
	function ProDel() {
		if (localStorage.getItem('currentUser') !== null) {
			goto('/update');
		}
	}
</script>

{#if localStorage.getItem('currentUser') !== null}
	<Navprod />
	<div class="text-center mt-5">
		<h1 class="mb-5">Perform Product CRUD operations Here!</h1>
		<button type="button" class="btn btn-primary" on:click={ProAdd}>Create</button>
		<button type="button" class="btn btn-danger" on:click={ProUp}>Delete</button>
		<button type="button" class="btn btn-success" on:click={ProDel}>Update</button>
	</div>
{:else}
	<a href="/register" class="btn bg-danger text-white">Click Here To Login Login</a>
{/if}
