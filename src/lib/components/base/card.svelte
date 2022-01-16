<script>
	export let url = null;
</script>

{#if url}
	<a
		class="card card-bordered text-primary-content bg-primary clickable"
		href={url}
		sveltekit:prefetch
	>
		{#if $$slots.image}
			<slot name="image" />
		{/if}
		<div class="body">
			<div class="content">
				<slot name="content" />
			</div>
			{#if $$slots.footer}
				<div class="footer">
					<slot name="footer" />
				</div>
			{/if}
		</div>
	</a>
{:else}
	<div class="card card-bordered text-primary-content bg-primary clickable">
		{#if $$slots.image}
			<slot name="image" />
		{/if}
		<div class="body">
			<div class="content">
				<slot name="content" />
			</div>
			{#if $$slots.footer}
				<div class="footer">
					<slot name="footer" />
				</div>
			{/if}
		</div>
	</div>
{/if}
