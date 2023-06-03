<script>
	import NavProd from '../navproducts/+page.svelte';
</script>

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
	<a href="/register" class="btn bg-danger text-white">Click Here To Login Login</a>
{/if}
