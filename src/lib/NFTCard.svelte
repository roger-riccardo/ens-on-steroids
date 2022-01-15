<script>
  export let name;
  export let tokenId;
  export let tokenUri;

  import { ethers } from "ethers";
  import { request, gql } from "graphql-request";

  const getENSInfo = async () => {
    const BigNumber = ethers.BigNumber;
    const labelHash = BigNumber.from(tokenId).toHexString();
    console.log(labelHash);
    const url = "https://api.thegraph.com/subgraphs/name/ensdomains/ens";
    const GET_LABEL_NAME = gql`
      query{
        registrations(first:1, where:{id:"${labelHash}"}){
          labelName
          registrationDate
          expiryDate
        }
      }`;
    return request(url, GET_LABEL_NAME).then((data) => {
      console.log("data:", data.registrations[0]);
      return data.registrations[0];
    });
  };
</script>

<div class="card text-center shadow-2xl">
  <figure class="px-10 pt-10">
    <img
      src="https://www.pngkit.com/png/full/152-1526200_ens-logo-ethereum-name-service.png"
      class="rounded-xl"
    />
  </figure>
  <div class="card-body">
    {name}
    {#await getENSInfo()}
      loading...
    {:then item}
      <h2 class="card-title">
        {item.labelName}.eth
      </h2>
      <div class="justify-center card-actions">
        Registration: {new Date(item.registrationDate * 1000).toLocaleString()}
      </div>
      <div class="justify-center card-actions">
        Expiration: {new Date(item.expiryDate * 1000).toLocaleString()}
      </div>
    {/await}
  </div>
</div>
