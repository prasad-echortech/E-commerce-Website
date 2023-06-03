<nav class="navbar navbar-expand-lg navbar-light bg-primary d-flex justify-content-between">
	<div class="container-fluid">
		<a class="navbar-brand" href="/">Ecommerce</a>
		<button
			class="navbar-toggler"
			type="button"
			data-bs-toggle="collapse"
			data-bs-target="#navbarSupportedContent"
			aria-controls="navbarSupportedContent"
			aria-expanded="false"
			aria-label="Toggle navigation"
		>
			<span class="navbar-toggler-icon" />
		</button>
		<div class="collapse navbar-collapse" id="navbarSupportedContent">
			<ul class="navbar-nav me-auto mb-2 mb-lg-0">
				<li class="nav-item">
					<a class="nav-link active" aria-current="page" href="/crud"
						><button class="btn bg-white text-success p-1 fw-bold">Products CRUD</button></a
					>
				</li>
				<li class="nav-item">
					<a class="nav-link active" aria-current="page" href="/cart"
						><button class="btn bg-white text-danger p-1 fw-bold">Cart 🛒</button>
					</a>
				</li>
				<li class="nav-item">
					<a class="nav-link active" aria-current="page" href="/products"
						><button class="btn bg-white text-danger p-1 fw-bold">Products</button>
					</a>
				</li>

				<li class="nav-item">
					<a class="nav-link active" aria-current="page" href="/checkout"
						><button class="btn bg-danger text-white p-1 fw-bold">Check-Out 💰</button>
					</a>
				</li>
				<li class="nav-item">
					<a class="nav-link active" aria-current="page" href="/logout"
						><button class="btn bg-danger text-white p-1 fw-bold">Log-Out</button>
					</a>
				</li>
			</ul>
			<form class="d-flex">
				<input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />
				<button class="btn bg-white fw-bold" type="submit">Search</button>
			</form>
		</div>
	</div>
</nav>
