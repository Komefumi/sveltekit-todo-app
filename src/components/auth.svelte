<script lang="ts">
	import { supabase } from '$lib';

	let loading = false;
	let email = '';

	async function handleLogin() {
		try {
			loading = true;
			const { error } = await supabase.auth.signInWithOtp({ email });
			if (error) {
				throw error;
			}
			alert('Check your email');
		} catch (error) {
			console.error(error);
		} finally {
			loading = false;
		}
	}
</script>

<h1 class="text-2xl font-bold text-center text-gray-800 md:text-3xl">Log In</h1>
<p class="text-center mt-2">Sign in via magic link with your email below.</p>
<form on:submit|preventDefault={handleLogin}>
	<div class="flex flex-col text-sm mb-2">
		<label class="font-bold mb-2 text-gray-800" for="email">Email</label>
		<input
			class="appearance-none shadow-sm border border-gray-200 p-2 focus:outline-none focus:border-gray-500 rounded-lg"
			type="email"
			name="email"
			placeholder="Your Email"
			bind:value={email}
			id=""
		/>
	</div>
	<button
		class="w-full shadow-sm rounded bg-blue-500 hover:bg-blue-600 text-white py-2 px-4"
		disabled={loading}
		type="submit"
	>
		Log In
	</button>
</form>
