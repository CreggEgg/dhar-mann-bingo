<script lang="ts">
    import { goto } from "$app/navigation";
    import { browser } from "$app/environment";
	import { page } from "$app/stores";
	import { PUBLIC_CLIENT_ID } from "$env/static/public";


    let params = new URLSearchParams($page.url.hash.slice(1));
    if (browser) {
        (async () => {
            let state = params.get("state")
            if(state !== localStorage.getItem("state")) {
                goto("/error/state")
            } else {
            const response = await fetch("https://api.twitch.tv/helix/users", {
                method: "GET",
                headers: {
                    "Authorization": `Bearer ${params.get("access_token")}`,
                    "Client-Id": PUBLIC_CLIENT_ID
                }
            })
            localStorage.username = (await response.json()).data[0].display_name
            goto("/")
        }
        })();
       //
    }
</script>

<h1></h1>