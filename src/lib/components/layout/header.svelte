<script>
	import Logo from '$lib/svg/logo.svelte';
	import Socials from '$lib/components/base/socials.svelte';
</script>

<header>
	<div id="navbar" class="navbar mb-2 shadow-lg bg-neutral text-neutral-content rounded-box">
		<div class="flex-1 px-2 mx-2">
			<span class="text-xl font-bold">
				<a id="home-btn" href="/" class="btn btn-ghost btn-sm rounded-btn"> ENS ON STEROIDS </a>
			</span>
		</div>
		<div class="flex-none hidden px-2 mx-2 lg:flex">
			<div class="flex items-stretch">
				<div class="grid grid-flow-col gap-4">
					<Socials />
				</div>
			</div>
		</div>
		<div class="flex-none">
			<button class="btn btn-square btn-ghost">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					class="inline-block w-6 h-6 stroke-current"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M4 6h16M4 12h16M4 18h16"
					/>
				</svg>
			</button>
		</div>
	</div>
</header>

<style lang="scss">
	@import '../../scss/breakpoints.scss';

	#navbar {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 15px;
		position: relative;

		@include for-phone-only {
			padding: 40px 0 50px;
		}
	}
</style>
