<script>
	import { page } from '$app/stores';
	import { browser } from '$app/environment';
	// import Navprods from "../../navproducts"

	const productId = $page.params.productsId;
	fetch(`http://localhost:3000/Products/${productId}`)
		.then((res) => res.json())
		.then(console.log())
		.then((res) => {
			myCardArr = [res];
		});
	let myCardArr = [];

	function cartData(cards) {
		function st() {
			alert('SuccessFully Added To 🛒 😊');
		}
		const setTime = setTimeout(st, -1000);

		fetch('http://localhost:3000/currentusercart', {
			method: 'POST',
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify({
				name: cards.name,
				price: cards.price,
				pid: cards.id,
				userid: userdata1.id
			})
		})
			.then((res) => res.json())
			.then(console.log);
		goto('/cart');
	}

	let userdata;
	let userdata1;
	if (browser) {
		userdata = localStorage.getItem('currentUser');
		userdata1 = JSON.parse(userdata);
	}
</script>

<div
	class="container-fluid d-flex flex-row flex-wrap text-center justify-content-center mt-5"
	id="wholecard"
>
	{#each myCardArr as cards}
		<div class="card ms-3 mb-3" style="width: 15rem;">
			<div class="card-body border border-success">
				<h5 class="card-title">Title : {cards.name}</h5>
				<h5 class="card-title">Product Id : {cards.id}</h5>
				<p class="card-text text-primary">
					Description : Lorem ipsum, dolor sit amet consectetur adipisicing elit. Expedita dolorem
					hic aut architecto perspiciatis magni adipisci quo nihil ea, unde facilis molestiae facere
					sint nam labore, quisquam minima excepturi exercitationem!
					<img
						src="https://i.pinimg.com/originals/a0/bb/5d/a0bb5dd5939d2497b99308604a403dbb.jpg"
						alt=""
						class="img-thumbnail"
					/>
				</p>
				<h5 class="card-title">Price: {cards.price} /-</h5>
				{#if browser}
					{#if localStorage.getItem('currentUser') !== null}
						<div>
							<a href="#" on:click={cartData(cards)} class="btn btn-primary mb-3">Add to Cart🛒</a>
						</div>
					{:else}
						<a href="/register" class="btn btn-primary mb-3">Add to Cart🛒</a>
					{/if}
				{/if}
			</div>
		</div>
	{/each}
</div>
