<script>
  import axios from "axios";
  import { intervalToDuration } from "date-fns";
  import { onMount } from "svelte";

  let items;

  async function getExpiringENS() {
    try {
      const result = await axios.post(
        "https://api.thegraph.com/subgraphs/name/ensdomains/ens",
        {
          query: `
					query getRegistrantFromSubgraph {
						registrations(
								first: 50,
								orderBy: expiryDate,
								orderDirection: asc,
								where: {
									expiryDate_gte: ${Math.round(new Date().getTime() / 1000)}
								}
						) {
								domain {
									id
									name
								}
								expiryDate
							}
						}
					`,
        }
      );

      const itemsWithCountdown = result.data.data.registrations.map((item) => {
        return {
          ...item,
          countdown: intervalToDuration({
            start: item.expiryDate * 1000,
            end: Date.now(),
          }),
        };
      });

      items = itemsWithCountdown;
    } catch (error) {
      console.error(error);
    }
  }

  onMount(() => {
    setInterval(() => {
      items = items.map((item) => {
        return {
          ...item,
          countdown: intervalToDuration({
            start: item.expiryDate * 1000,
            end: Date.now(),
          }),
        };
      });
    }, 1000);
  });
</script>

<section id="about">
  <div class="overflow-x-auto">
    <table class="table w-full table-zebra">
      <thead>
        <tr>
          <th />
          <th>ENS Domain</th>
          <th>Countdown</th>
          <th>Expiration Date</th>
          <th>Useful Links</th>
        </tr>
      </thead>
      <tbody>
        {#await getExpiringENS()}
          <p>Loading...</p>
        {:then expiringENS}
          {#each items as item, index}
            <tr>
              <th>{index + 1}</th>
              <td>{item.domain.name}</td>
              <td>
                <div
                  class="grid grid-flow-col gap-5 place-items-end auto-cols-max"
                >
                  <span class="font-mono text-2xl countdown">
                    <span style="--value:{item.countdown.hours || 0};" />h
                    <span style="--value:{item.countdown.minutes || 0};" />m
                    <span style="--value:{item.countdown.seconds || 0};" />s
                  </span>
                </div>
              </td>
              <td>{new Date(item.expiryDate * 1000).toLocaleString()}</td>
              <td>
                <a
                  class="link"
                  href="https://app.ens.domains/name/{item.domain.name}/details"
                  >ENS Domains</a
                >
                <a
                  class="link"
                  href="https://opensea.io/collection/ens?search[query]={item
                    .domain.name}">Opensea</a
                >
              </td>
            </tr>
          {/each}
        {/await}
      </tbody>
    </table>
  </div>
</section>
