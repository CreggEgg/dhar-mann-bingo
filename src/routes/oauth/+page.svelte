<script>
	import { goto } from "$app/navigation";
    import { browser } from "$app/environment";
    import {v4} from "uuid";
    import { PUBLIC_CLIENT_ID, PUBLIC_REDIRECT_URI } from '$env/static/public'

    
    if(browser) {
        let state = v4();
        localStorage.state = state;
        goto(`https://id.twitch.tv/oauth2/authorize?response_type=token&client_id=${PUBLIC_CLIENT_ID}&redirect_uri=${PUBLIC_REDIRECT_URI}&scope=${encodeURI("user:read:email")}&state=${state}`)
    
    }
</script>