<script>
	import { browser } from '$app/environment';
	import Navprod from '../navproducts/+page.svelte';
	import { goto } from '$app/navigation';

	fetch(`http://localhost:3000/currentusercart`)
		.then((res) => res.json())
		.then((res) => {
			mycurrentusercart = [...res];
			mycurrentusercart.map((item) => {
				if (browser) if (item.userid == userdata1.id) sum += item.price;
				console.log(item.price);
			});
		});

	let mycurrentusercart = [];
	let sum = 0;

	function remover(id) {
		location.reload();
		// alert('SuccessFully Removed From Existing Products 🛒 😥');
		fetch(` http://localhost:3000/currentusercart/${id}`, {
			method: 'DELETE'
		}).then((res) => res.json());
	}

	let userdata;
	let userdata1;
	if (browser) {
		userdata = localStorage.getItem('currentUser');
		userdata1 = JSON.parse(userdata);
	}

	function pay() {
		goto('/payment');
	}
</script>

{#if userdata1 !== null}
	<Navprod />
	<h1 class="text-center mt-3">Welcome to Final CheckOut Step💰</h1>
	<h1 class="text-center mt-5 mb-5">Your Products 😍</h1>
	<table class="table border-dark fw-bold">
		<thead>
			<tr class="fs-4">
				<th scope="col">#</th>
				<th scope="col">Product Name</th>
				<th scope="col">Price</th>
				<th scope="col">Id</th>
				<th scope="col">U-Id</th>
				<th scope="col">Remove</th>
			</tr>
		</thead>
		{#each mycurrentusercart as data}
			{#if data.userid === userdata1.id}
				<tbody>
					<tr>
						<td>*</td>
						<td>{data.name}</td>
						<td>{data.price}</td>
						<td>{data.id}</td>
						<td>{data.userid}</td>

						<td
							><button class="btn bg-danger text-white" on:click={remover(data.id)}>Remove</button
							></td
						>
					</tr>
				</tbody>
			{/if}
		{/each}
	</table>
	<h1 class="text-center border border-dark">
		Total Amount: <span class="text-success"> {sum} /- </span>
	</h1>

	<div class="text-center mt-5">
		<a href="#">
			<button class="btn bg-success text-white ms-5 mb-5 fs-3" on:click={pay}> Pay 💵</button>
		</a>
	</div>
{:else}
	<a href="/register" class="btn bg-danger text-white">Click Here To Login Login</a>
{/if}
