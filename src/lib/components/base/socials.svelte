<script>
	import TelegramIcon from '../../svg/socials/telegram.svelte';
	import TwitterIcon from '../../svg/socials/twitter.svelte';
	//import YouTubeIcon from '$lib/svg/socials/youtube.svelte';
	import GitHubIcon from '../../svg/socials/github.svelte';
	import EmailIcon from '../../svg/socials/email.svelte';
</script>

<div class="socials">
	<a
		id="twitter-btn"
		href={'https://twitter.com/r_persiani1'}
		class="btn btn-ghost btn-sm rounded-btn"
	>
		<TwitterIcon />
	</a>
	<a
		id="github-btn"
		href={'https://github.com/roger-riccardo'}
		class="btn btn-ghost btn-sm rounded-btn"
	>
		<GitHubIcon />
	</a>
	<a
		id="email-btn"
		href={'mailto:r.persiani@protonmail.com'}
		class="btn btn-ghost btn-sm rounded-btn"
	>
		<EmailIcon />
	</a>
	<a
		id="telegram-btn"
		href={'https://telegram.me/RiccardoPersiani'}
		class="btn btn-ghost btn-sm rounded-btn"
	>
		<TelegramIcon />
	</a>
</div>
