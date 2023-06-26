<script>
	import Crud from '../crud/+page.svelte';
	import { browser } from '$app/environment';

	let name = '';
	let price;
	let id = Math.floor(Math.random() * 1000);
	console.log(id);

	let handleSubmit = async () => {
		if (name != '' && price != '' && id != '') {
			// valid credientials submit form data
			const userData = { name, price, id };

			try {
				const response = await fetch('http://localhost:3000/products', {
					method: 'POST',
					headers: {
						'Content-Type': 'application/json'
					},
					body: JSON.stringify(userData)
				});
				if (response.ok) {
					console.log('form data stored successfully');
					//reset fields
					// id = '';
					name = '';
					price = '';
				} else {
					console.log('form data storage failed');
				}
			} catch (error) {
				console.log('an error occured', error);
			}
		}
	};
</script>
<Crud />
{#if browser}
{#if localStorage.getItem('currentUser') !== null}
<main><h1 class="mt-4">Create a New Product to Sell</h1></main>
<div class="d-flex justify-content-center mt-5 w-100">
	<form on:submit|preventDefault={handleSubmit}>
		<div class="mb-3">
			<label for="name" class="form-label">Product Name</label>
			<input
				placeholder="Product Name"
				type="text"
				class="form-control"
				id="name"
				bind:value={name}
			/>

			<div class="mb-3">
				<label for="password" class="form-label">Price</label>
				<input
					placeholder="Price"
					type="number"
					class="form-control"
					id="price"
					bind:value={price}
				/>
			</div>
			<div class="mb-3">
				<label for="password" class="form-label">Id</label>
				<input placeholder="id number" type="number" class="form-control" id="id" bind:value={id} />
			</div>
			<button type="submit" class="btn btn-primary">Add Product</button>
		</div>
	</form>
</div>
{/if}
{/if}
<style>
	main {
		text-align: center;
	}
</style>
