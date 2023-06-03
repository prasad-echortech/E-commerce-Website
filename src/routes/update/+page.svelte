<script>
	import Crud from '../crud/+page.svelte';
	let id;
	let name;
	let price;
	function update() {
		fetch(`http://localhost:3000/products/${id}`, {
			method: 'PUT' /* or PATCH */,
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify({
				name,
				price
			})
		})
			.then((res) => res.json())
			.then(console.log);
		id = '';
		name = '';
		price = '';
	}
</script>

<Crud />
<div class="text-center">
	<h1>Delete Your Products Here</h1>
	<div class="d-flex justify-content-center mt-5 w-100">
		<form on:submit|preventDefault={update}>
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
					<input
						placeholder="Id number"
						type="number"
						class="form-control"
						id="id"
						bind:value={id}
					/>
				</div>
				<button type="submit" class="btn btn-success">Update</button>
			</div>
		</form>
	</div>
</div>
