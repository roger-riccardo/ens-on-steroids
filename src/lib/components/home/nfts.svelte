<script>
	import { onMount } from 'svelte';
    import NFTCard from '$lib/components/layout/nft-card.svelte'

	let nfts = [];

	onMount(async () => {
        console.log("getting nfts")
		nfts = await getNFTs();
	});

	async function getNFTs() {
        const currentUser = Moralis.User.current();
console.log("current user:",currentUser)
		const options = {
			chain: 'eth',
			address: '0x953ad29773a115fa5f621c2b74500dc14bca7d77'
		};
		const res = await Moralis.Web3API.account.getNFTs(options);
		return res.result;
	}
</script>

<section id="about">
    <div class="grid grid-cols-3 mx-auto px-4 md:max-w-10xl">
        {#each Object.entries(nfts) as [key, item]}
          <NFTCard
            name={item.name}
            tokenId={item.token_id}
            tokenUri={item.token_uri}
          />
        {/each}
      </div>
</section>

<style lang="scss">
	@import '../../scss/breakpoints.scss';

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
