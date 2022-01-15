<script>
  import { request, gql } from "graphql-request";

  const getENSLongestExpiration = async () => {
    const url = "https://api.thegraph.com/subgraphs/name/ensdomains/ens";
    const GET_LABEL_NAME = gql`
      query{
        registrations(
                first:10, 
                orderBy: expiryDate, 
                orderDirection: desc,
                where: {
                    expiryDate_gt: 2247919454
                }
            ) {
                labelName
                registrationDate
                expiryDate       
                cost
                registrant {
                  id
                }
            }
      }`;
    return request(url, GET_LABEL_NAME).then((data) => {
      console.log("data2:", data.registrations);
      return data.registrations;
    });
  };

  const getENSInfo = async () => {
    const url = "https://api.thegraph.com/subgraphs/name/ensdomains/ens";
    const GET_LABEL_NAME = gql`
      query{
        registrations(
                first:10, 
                orderBy: cost, 
                orderDirection: desc,
                where: {
                    cost_gte: 1000000000000000000
                }
            ){
                labelName
                registrationDate
                expiryDate
                cost
                registrant {
                    id
                }
            }
      }`;
    return request(url, GET_LABEL_NAME).then((data) => {
      console.log("data:", data.registrations);
      return data.registrations;
    });
  };
</script>

<div>
<section id="about2">
    Longest Expiration
    <div class="overflow-x-auto">
      <table class="table w-full table-zebra">
        <thead>
          <tr>
            <th />
            <th>ENS Domain</th>
            <th>Registrant</th>
            <th>Avatar</th>
            <th>Expiration Date</th>
            <th>Useful Links</th>
          </tr>
        </thead>
        <tbody>
          {#await getENSLongestExpiration()}
            <p>Loading...</p>
          {:then items}
            {#each items as item, index}
              <tr>
                <th>{index + 1}</th>
                <td>{item.labelName}.eth</td>
                <td>{item.registrant.id}</td>
                <td>
                  <div class="flex-none">
                      <div class="avatar">
                        <div class="rounded-full w-lg h-lg m-1">
                          <img
                            src="https://publish.one37pm.net/wp-content/uploads/2021/02/punks.png?fit=600%2C600"
                          />
                        </div>
                      </div>
                    </div>
                </td>
                <td>{new Date(item.expiryDate * 1000).toLocaleString()}</td>
                <td>
                  <a
                    class="link"
                    href="https://app.ens.domains/name/{item.labelName}.eth/details"
                    >ENS Domains</a
                  >
                  <a
                    class="link"
                    href="https://opensea.io/collection/ens?search[query]={item
                      .labelName}">Opensea</a
                  >
                </td>
              </tr>
            {/each}
          {/await}
        </tbody>
      </table>
    </div>
  </section>
<section id="about">
  The highest cost
  <div class="overflow-x-auto">
    <table class="table w-full table-zebra">
      <thead>
        <tr>
          <th />
          <th>ENS Domain</th>
          <th>Cost</th>
          <th>Registrant</th>
          <th>Avatar</th>
          <th>Expiration Date</th>
          <th>Useful Links</th>
        </tr>
      </thead>
      <tbody>
        {#await getENSInfo()}
          <p>Loading...</p>
        {:then items}
          {#each items as item, index}
            <tr>
              <th>{index + 1}</th>
              <td>{item.labelName}.eth</td>
              <td>{(item.cost / 1000000000000000000).toFixed(2)} ETH</td>
              <td>{item.registrant.id}</td>
              <td>
                <div class="flex-none">
                    <div class="avatar">
                      <div class="rounded-full w-lg h-lg m-1">
                        <img
                          src="https://publish.one37pm.net/wp-content/uploads/2021/02/punks.png?fit=600%2C600"
                        />
                      </div>
                    </div>
                  </div>
              </td>
              <td>{new Date(item.expiryDate * 1000).toLocaleString()}</td>
              <td>
                <a
                  class="link"
                  href="https://app.ens.domains/name/{item.labelName}.eth/details"
                  >ENS Domains</a
                >
                <a
                  class="link"
                  href="https://opensea.io/collection/ens?search[query]={item
                    .labelName}">Opensea</a
                >
              </td>
            </tr>
          {/each}
        {/await}
      </tbody>
    </table>
  </div>
</section>
</div>
