<script>
	import { browser } from '$app/environment';
	import { goto } from '$app/navigation';
	import Navprod from '../navproducts/+page.svelte';

	
	function ProAdd() {
		if (browser) {
			if (localStorage.getItem('currentUser') !== null) {
				goto('/add');
			}
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
{#if browser}
{#if localStorage.getItem('currentUser') !== null}

	<Navprod />
	<div class="text-center mt-5">
		<h1 class="mb-5">Perform Product CRUD operations Here!</h1>
		<button type="button" class="btn btn-primary" on:click={ProAdd}>Create</button>
		<button type="button" class="btn btn-danger" on:click={ProUp}>Delete</button>
		<button type="button" class="btn btn-success" on:click={ProDel}>Update</button>
	</div>
{:else}
	<div class=" mt-5 text-center">
		<a href="/register" class=" text-white mt-5 btn btn-danger mb-5"> Click here To Login</a>
		<h1>Please Login or Register 😊</h1>
	</div>
	{/if}
{/if}

