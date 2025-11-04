<script lang="ts">
	let showLoginForm = $state(false);

	function toggleLoginForm() {
		showLoginForm = !showLoginForm;
	}

	function handleLogin(event: Event) {
		event.preventDefault();
		alert("Login submitted!");
		showLoginForm = false;
	}
</script>

<div class="min-h-screen bg-gradient-to-br from-blue-500 to-purple-600 font-sans text-gray-800">
	<div class="container mx-auto px-4">
		<section class="text-center py-20 text-white">
			<h1 class="text-5xl font-bold mb-6 drop-shadow-lg">
				Welcome to Our Amazing App
			</h1>
			<p class="text-xl mb-10 opacity-90">
				Discover the power of modern web development with our
				cutting-edge platform. Join thousands of users who trust us for
				their digital needs.
			</p>

			<button
				class="bg-gradient-to-r from-red-400 to-orange-500 text-white px-8 py-4 rounded-full text-lg font-semibold cursor-pointer transition-all duration-300 shadow-lg hover:shadow-xl hover:-translate-y-1"
				onclick={toggleLoginForm}
			>
				Get Started - Login
			</button>
		</section>

		<section class="py-20 bg-white/10 backdrop-blur-md rounded-3xl my-10">
			<div class="container mx-auto px-4">
				<h2 class="text-center text-white text-4xl font-bold mb-12">
					Why Choose Us?
				</h2>

				<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
					<div class="bg-white/20 p-8 rounded-2xl text-center transition-transform duration-300 hover:-translate-y-2 backdrop-blur-sm">
						<h3 class="text-white text-2xl font-semibold mb-4">Lightning Fast</h3>
						<p class="text-white/80">
							Experience blazing-fast performance with our optimized infrastructure.
						</p>
					</div>

					<div class="bg-white/20 p-8 rounded-2xl text-center transition-transform duration-300 hover:-translate-y-2 backdrop-blur-sm">
						<h3 class="text-white text-2xl font-semibold mb-4">Secure & Reliable</h3>
						<p class="text-white/80">
							Your data is protected with enterprise-grade security measures.
						</p>
					</div>

					<div class="bg-white/20 p-8 rounded-2xl text-center transition-transform duration-300 hover:-translate-y-2 backdrop-blur-sm">
						<h3 class="text-white text-2xl font-semibold mb-4">User-Friendly</h3>
						<p class="text-white/80">
							Intuitive design that makes complex tasks simple and enjoyable.
						</p>
					</div>
				</div>
			</div>
		</section>

		<footer class="text-center py-10 text-white/70">
			<p>&copy; 2025 Our Amazing App. All rights reserved.</p>
		</footer>
	</div>

	{#if showLoginForm}
		<div
			class="fixed inset-0 bg-black/50 flex items-center justify-center z-50"
			onclick={(e) => {
				// Only close if background (overlay) is clicked
				if (e.target === e.currentTarget) toggleLoginForm();
			}}
			onkeydown={(e) => {
				if (e.key === "Escape") toggleLoginForm();
			}}
			role="dialog"
			aria-modal="true"
			aria-labelledby="login-title"
			tabindex="-1"
		>
			<form
				class="bg-white p-10 rounded-3xl shadow-2xl w-full max-w-md mx-4 relative"
				onsubmit={handleLogin}
			>
				<button
					type="button"
					class="absolute top-4 right-4 text-gray-400 hover:text-gray-600 text-2xl"
					onclick={toggleLoginForm}
					aria-label="Close login form"
				>
					&times;
				</button>

				<h2
					id="login-title"
					class="text-center text-2xl font-bold mb-8 text-gray-800"
				>
					Login to Your Account
				</h2>

				<div class="mb-6">
					<label for="email" class="block text-gray-700 font-medium mb-2">
						Email
					</label>
					<input
						type="email"
						id="email"
						class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 transition-colors"
						placeholder="Enter your email"
						required
					/>
				</div>

				<div class="mb-6">
					<label for="password" class="block text-gray-700 font-medium mb-2">
						Password
					</label>
					<input
						type="password"
						id="password"
						class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 transition-colors"
						placeholder="Enter your password"
						required
					/>
				</div>

				<button
					type="submit"
					class="w-full bg-gradient-to-r from-blue-500 to-purple-600 text-white py-3 rounded-lg font-semibold transition-all duration-300 hover:shadow-lg hover:-translate-y-1"
				>
					Login
				</button>
			</form>
		</div>
	{/if}
</div>
