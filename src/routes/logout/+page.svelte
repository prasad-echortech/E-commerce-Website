<script>
	import { browser } from '$app/environment';
	import { goto } from '$app/navigation';
	if (browser) {
		function to() {
			localStorage.removeItem('currentUser');
			alert('Successfully Logged Out');
		}
		const timeOut = setTimeout(to, 2000);
	}
	goto('/');
</script>

<h1>Successfully logged Out</h1>
