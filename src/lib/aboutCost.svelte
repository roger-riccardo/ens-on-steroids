<script>
	import SparklingHighlight from './style/sparkling-highlight.svelte';
</script>

<section id="about">
	<div class="info">
		<h2>
			The ENS domains
			<SparklingHighlight>MOST EXPENSIVE</SparklingHighlight>
		</h2>
	</div>
</section>

<style lang="scss">
	@import './scss/breakpoints.scss';

#about {
	position: relative;
	display: flex;
	grid-template-columns: 500px 250px;
	align-items: center;
	justify-content: center;
	gap: 15px;
	padding: 80px 0;

	@include for-phone-only {
		grid-template-columns: 1fr;
		justify-items: center;
	}

	.info {
		display: flex;
		flex-direction: column;
		gap: 10px;
		h2 {
			@include for-phone-only {
				text-align: center;
			}
		}

		p {
			@include for-phone-only {
				text-align: justify;
			}
		}
	}
}

@keyframes spin {
	from {
		transform: rotate(0turn);
	}
	to {
		transform: rotate(1turn);
	}
}
</style>
