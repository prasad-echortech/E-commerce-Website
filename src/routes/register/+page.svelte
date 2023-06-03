<script>
	import { goto } from '$app/navigation';
	import Nav from '../nav/+page.svelte';

	let name = '';
	let password = '';
	// let id = Math.floor(Math.random() * 1000);
	// console.log(id);

	const handleSubmit = async () => {
		// valid credientials submit form data
		const userData = { name, password };

		try {
			const response = await fetch('http://localhost:3000/users', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},
				body: JSON.stringify(userData)
			});
			if (response.ok) {
				console.log('form data stored successfully');
				//reset fields
				name = '';
				password = '';
				goto('/login');
			} else {
				console.log('form data storage failed');
			}
		} catch (error) {
			console.log('an error occured', error);
		}
	};
</script>

<Nav />
<main><h1>Register Here?</h1></main>
<div class="d-flex justify-content-center mt-5 w-100">
	<form on:submit|preventDefault={handleSubmit}>
		<div class="mb-3">
			<label for="name" class="form-label">User Name</label>
			<input placeholder="name" type="text" class="form-control" id="name" bind:value={name} />

			<div class="mb-3">
				<label for="password" class="form-label">Password</label>
				<input
					placeholder="Password"
					type="password"
					class="form-control"
					id="password"
					bind:value={password}
				/>
			</div>
			<button type="submit" class="btn btn-primary">Submit</button>
		</div>
	</form>
</div>
<div class="text-center">
	Already Registered <a href="/login">login</a>
</div>

<style>
	main {
		text-align: center;
	}
</style>
