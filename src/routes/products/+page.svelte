<script>
	import { browser } from '$app/environment';
	import { goto } from '$app/navigation';
	import NavProd from '../navproducts/+page.svelte';
	import { onMount, afterUpdate } from 'svelte';
	import { writable, derived } from 'svelte/store';

	const pageSize = 5; // Number of items per page
	const dataset = writable([]); // Your dataset goes here

	// Calculate the number of pages
	const totalPages = derived(dataset, ($dataset) => Math.ceil($dataset.length / pageSize));

	// Current page store
	const currentPage = writable(1);

	// Computed property to slice the dataset based on the current page
	const paginatedData = derived([dataset, currentPage], ([$dataset, $currentPage]) => {
		const start = ($currentPage - 1) * pageSize;
		const end = start + pageSize;
		return $dataset.slice(start, end);
	});

	onMount(async () => {
		const response = await fetch('http://localhost:3000/Products');
		const data = await response.json();
		dataset.set(data);
	});

	let myCardArr = [];

	// Update myCardArr whenever paginatedData changes
	afterUpdate(() => {
		myCardArr = $paginatedData;
	});

	// Handle page navigation
	function goToPage(page) {
		currentPage.set(page);
	}
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
		goto('/products');
	}
	let userdata;
	let userdata1;
	if (browser) {
		userdata = localStorage.getItem('currentUser');
		userdata1 = JSON.parse(userdata);
		console.log(userdata1.id);
	}

	// 	let condition = localStorage.getItem("currentUser") === null;

	// 	onMount(() => {
	//     if (!condition) {
	//       push('/other'); // Navigate to the "Other Page" when the condition is false
	//     }
	//   });
</script>

{#if userdata1 != null}
	<NavProd />
	<a href="/cart" class="ms-5">
		<button class=" btn bg-success text-white mt-3">Go to Cart🛒</button>
	</a>

	<div
		class="container-fluid d-flex flex-row flex-wrap text-center justify-content-center mt-2"
		id="wholecard"
	>
		{#each myCardArr as cards}
			<div class="card ms-3 mb-3" style="width: 15rem;">
				<div class="card-body border border-success">
					<h5 class="card-title">Title : {cards.name}</h5>
					<h5 class="card-title">Product Id : {cards.id}</h5>
					<p class="card-text text-primary">
						Description : Lorem ipsum, dolor sit amet consectetur adipisicing elit. Expedita dolorem
						hic aut architecto perspiciatis magni adipisci quo nihil ea, unde facilis molestiae
						facere sint nam labore, quisquam minima excepturi exercitationem!
						<img
							src="https://i.pinimg.com/originals/a0/bb/5d/a0bb5dd5939d2497b99308604a403dbb.jpg"
							alt=""
							class="img-thumbnail"
						/>
					</p>
					<h5 class="card-title">Price: {cards.price} /-</h5>
					<div>
						<a href="#" on:click={cartData(cards)} class="btn btn-primary mb-3">Add to Cart🛒</a>
						<!-- <button class="btn bg-danger fs-6 p-0 mb-3 tet-white">info</button> -->
					</div>
				</div>
			</div>
		{/each}
	</div>
{:else}
<div class=" mt-5 text-center">
	<a href="/register" class=" text-white mt-5 btn btn-danger mb-5"> Click here To Login</a>
	<h1>Please Login or Register 😊</h1>
</div>
{/if}

<!-- Display pagination controls -->
<div class="text-center mt-4 mb-3">
	{#each Array.from({ length: $totalPages }) as _, i}
		<button class="btn btn-dark m-1 shadow-lg" on:click={() => goToPage(i + 1)}> {i + 1} </button>
	{/each}
</div>
