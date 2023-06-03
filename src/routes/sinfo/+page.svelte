<script>
	import { browser } from '$app/environment';
	import { goto } from '$app/navigation';

	let userdata;
	let userdata1;
	if (browser) {
		userdata = localStorage.getItem('UsrInfoID');
		userdata1 = JSON.parse(userdata);
		console.log(userdata1);
		// function to() {
		// 	localStorage.removeItem('UsrInfoID');
		// 	goto('/');
		// }
		// const timeOut = setTimeout(to, 10000);
	}
	(async () => {
		let res = await fetch(`http://localhost:3000/Products/${userdata1}`)
			.then((res) => res.json())
			.then((res) => {
				myCardArr = [res];
			});
	})();

	let myCardArr = [];
</script>

<h1>Welcome to The Single Product Page:</h1>

<div class="text-center">
	Register Here<a href="/register"> Click?</a> Already Registered <a href="/login">login</a>
</div>
<div
	class="container-fluid d-flex flex-row flex-wrap text-center justify-content-center mt-5"
	id="wholecard"
>
	{#each myCardArr as cards}
		<div class="card ms-3 mb-2" style="width: 15rem;">
			<div class="card-body border border-success">
				<h5 class="card-title">Title : {cards.name}</h5>
				<h5 class="card-title">Product-Id : {cards.id}</h5>
				<p class="card-text">
					Lorem ipsum, dolor sit amet consectetur adipisicing elit. Expedita dolorem hic aut
					architecto perspiciatis magni adipisci quo nihil ea, unde facilis molestiae facere sint
					nam labore, quisquam minima excepturi exercitationem!
				</p>
				<h5 class="card-title">Price : {cards.price}/-</h5>
				<div>
					<a href="/register" class="btn btn-primary mb-3">Add to Cart🛒</a>
				</div>
				<a href="/">
					<button class="btn btn-secondary">Go To Home</button>
				</a>
			</div>
		</div>
	{/each}
</div>
