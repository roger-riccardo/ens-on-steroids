<script>
  import NFTCard from "../lib/NFTCard.svelte";
  import { onMount } from "svelte";

  let nfts = [];

  onMount(async () => {
    nfts = await getNFTs();
  });

  async function getNFTs() {
    if (Moralis.User.current()) {
      const options = {
        chain: "eth",
        address: Moralis.User.current().attributes.accounts[0],
        token_address: "0x57f1887a8bf19b14fc0df6fd9b2acc9af147ea85",
      };
      const res = await Moralis.Web3API.account.getNFTsForContract(options);
      return res.result;
    }
  }
</script>

<div class="grid grid-cols-3 mx-auto px-4 md:max-w-10xl">
  {#each Object.entries(nfts) as [key, item]}
    <NFTCard
      name={item.name}
      tokenId={item.token_id}
      tokenUri={item.token_uri}
    />
  {/each}
</div>
