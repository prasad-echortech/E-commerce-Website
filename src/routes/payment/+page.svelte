<script>
	import NavProd from '../navproducts/+page.svelte';
	import { browser } from '$app/environment';
</script>

{#if browser}
	{#if localStorage.getItem('currentUser') !== null}
		<NavProd />
		<div class="text-center mt-5">
			<h1>Welcome We Accept All Payment Modes</h1>
			<img
				src="https://i0.wp.com/cashfree.com/blog/wp-content/uploads/2018/04/payment_gateway5.png?resize=954%2C464&ssl=1"
				alt=""
			/>
			<h1>We Will Deliver The Order Soon 🚚</h1>
			<img
				class=""
				src="https://media.tenor.com/lXOv8L5pgU0AAAAM/sepiring-padang-delivery.gif"
				alt="Rider"
			/>
		</div>
	{:else}
		<div class=" mt-5 text-center">
			<a href="/register" class=" text-white mt-5 btn btn-danger mb-5"> Click here To Login</a>
			<h1>Please Login or Register 😊</h1>
		</div>{/if}
{/if}
