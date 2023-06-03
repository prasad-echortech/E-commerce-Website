<!-- <script>
	import { page } from '$app/stores';
	const productId = $page.params.productsId;
	
	fetch(`http://localhost:3000/Products${productId}`)
		.then((res) => res.json())
		.then((res) => {
			productInfo = JSON.parse(res);
           
		});
        let productInfo;
</script>

<div>
	<h1>Welocme To Single Product {productId}</h1>
</div>

<div
	class="container-fluid d-flex flex-row flex-wrap text-center justify-content-center mt-2"
	id="wholecard"
>

	<div class="card ms-3 mb-3" style="width: 15rem;">
		<div class="card-body border border-success">
			<h5 class="card-title">Title : {productInfo.name}</h5>
			<h5 class="card-title">Product Id : {productInfo.id}</h5>
			<p class="card-text text-primary">
				Description : Lorem ipsum, dolor sit amet consectetur adipisicing elit. Expedita dolorem hic
				aut architecto perspiciatis magni adipisci quo nihil ea, unde facilis molestiae facere sint
				nam labore, quisquam minima excepturi exercitationem!
				<img
					src="https://i.pinimg.com/originals/a0/bb/5d/a0bb5dd5939d2497b99308604a403dbb.jpg"
					alt=""
					class="img-thumbnail"
				/>
			</p>
			<h5 class="card-title">Price: {productInfo.price} /-</h5>
			<div>
				
			</div>
		</div>
	</div>
  
</div> -->
