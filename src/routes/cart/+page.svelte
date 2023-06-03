<script>
	import { browser } from '$app/environment';
	import NavProd from '../navproducts/+page.svelte';

	(async () => {
		let res = await fetch(`http://localhost:3000/currentusercart`)
			.then((res) => res.json())
			.then((res) => res);
		mycurrentusercart = [...res];
	})();
	let mycurrentusercart = [];

	let userdata;
	let userdata1;
	if (browser) {
		userdata = localStorage.getItem('currentUser');
		userdata1 = JSON.parse(userdata);
	}

	function remover(id) {
		function st() {
			location.reload();
			alert('SuccessFully Removed From Cart 🛒 😥');
			// Refresh the page
		}
		const setTime = setTimeout(st, -1000);
		fetch(` http://localhost:3000/currentusercart/${id}`, {
			method: 'DELETE'
		}).then((res) => res.json());
	}

	let amoutTotal = 0;
	console.log(amoutTotal);
</script>
{#if userdata1 != null}
<NavProd />
<div>
	<a href="/products">
		<button class=" btn bg-success text-white mt-3 ms-5">Goto Products</button>
	</a>
</div>
<h1 class="text-center mt-5">Your Cart</h1>
<div
	class="container-fluid d-flex flex-row flex-wrap text-center justify-content-center mt-5"
	id="wholecard"
>
	{#each mycurrentusercart as cards}
		{#if userdata1.id == cards.userid}
			{#if cards.name}
				<div class="card ms-3 mb-3" style="width: 15rem;">
					<div class="card-body border border-success">
						<h5 class="card-title">Title : {cards.name}</h5>
						<h5 class="card-title">Product Id : {cards.id}</h5>
						<h5 class="card-title">User Id : {cards.userid}</h5>
						<p class="card-text">
							Lorem ipsum, dolor sit amet consectetur adipisicing elit. Expedita dolorem hic aut
							architecto perspiciatis magni adipisci quo nihil ea, unde facilis molestiae facere
							sint nam labore, quisquam minima excepturi exercitationem!
						</p>
						<h5 class="card-title">Price : {cards.price} /-</h5>
						<div>
							<button class=" btn bg-danger text-white" on:click={remover(cards.id)}>Remove</button>
						</div>
					</div>
				</div>
			{/if}
		{/if}
	{/each}
</div>
<div class="text-center mt-5">
	<a href="/checkout">
		<button class="btn bg-success text-white ms-5 mb-5 fs-3"> Checkout 💵</button>
	</a>
</div>

{:else}
	<a href="/register" class="btn bg-danger text-white">Click Here To Login Login</a>
{/if}