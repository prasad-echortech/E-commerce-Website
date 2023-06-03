<script>
	import Nav from '../nav/+page.svelte';
	import { goto } from '$app/navigation';

	let errorMsg = '';
	let login = {
		name: '',
		password: ''
	};
	async function bcheck() {
		fetch('http://localhost:3000/users')
			.then((res) => res.json())
			.then((res) =>
				res.forEach((element) => {
					if (element.name === login.name && element.password === login.password) {
						// alert("Login Successful")
						JSON.stringify(element);
						localStorage.setItem('currentUser', JSON.stringify(element));
						goto('/products');
					} else {
					}
				})
			)
			.catch((e) => {
				console.log('eerr', e);
			});
	}
</script>

<Nav />

<main><h1>Login Here!</h1></main>
<div class="w-100 d-flex justify-content-center mt-5">
	<form>
		<div class="mb-3">
			<label for="name" class="form-label">User Name</label>
			<input
				placeholder="name"
				type="text"
				class="form-control"
				id="name"
				bind:value={login.name}
			/>

			<div class="mb-3">
				<label for="password" class="form-label">Password</label>
				<input
					placeholder="Password"
					type="password"
					class="form-control"
					id="password"
					bind:value={login.password}
				/>
			</div>
			<button type="submit" class="btn btn-primary" on:click={bcheck}>Login</button>
			<h1>{errorMsg}</h1>
		</div>
	</form>
</div>

<style>
	main {
		text-align: center;
	}
</style>
