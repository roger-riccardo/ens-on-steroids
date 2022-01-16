<script>
    export let name;
    export let tokenId;
    export let tokenUri;
    
    async function getImage(_tokenUri) {
        try {
            const proxy = "http://127.0.0.1:8080/"
            const response = await fetch(proxy + _tokenUri, {
                mode: 'cors',
                headers: {
                    'Access-Control-Allow-Origin': '*'
                }
            });
            const myJson = await response.json(); //extract JSON from the http response
            const image = myJson.image
            if (image.includes("ipfs://")) {
                const test = image.split("ipfs://").pop();
                return "https://ipfs.io/ipfs/" + test;
            }
            return myJson.image;
        } catch (e) {
            try {
                const response = await fetch(_tokenUri);
                const myJson = await response.json(); //extract JSON from the http response
                const image = myJson.image
                if (image.includes("ipfs://")) {
                    const test = image.split("ipfs://").pop();
                    return myJson.image;
                }
                return myJson.image;
            } catch (e2) {
                console.log("error in getting image 2:", e2);
            }
        }
    }
    </script>
    
    <div class="p-2 m-3 border-2 h-20px">
        {#await getImage(tokenUri)}
        {console.log("loading img...")}
        {:then image}
        <div class="h-20px w-full">
            {#if image}
            <img class="bg-gray-100 h-xl object-contain w-full" src={image} />
            {:else}
            <img
                class="bg-gray-100 h-xl object-contain w-full"
                />
            {/if}
        </div>
        {/await}
        <div class="card-body">
            <h2 class="card-title">
                {name}
                <div class="badge mx-2 badge-secondary">
                    {tokenId}
                </div>
            </h2>
        </div>
    </div>
    