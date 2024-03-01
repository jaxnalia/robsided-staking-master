<script>
	import { TwitterLogo, DiscordLogo, PaperPlane, GithubLogo } from 'radix-icons-svelte';
	import rob from '../../images/rob.png';
	const footStyle =
		'sticky top-0 z-40 w-full px-3 pt-4 lg:px-9';
	const link = {
		tele: '',
		xapp: 'https://x.com/shaneheartwin',
		chart: 'https://dexscreener.com/pulsechain/0x87791dd63ecfb326768630e7ae3a3497f295b656',
		swap: 'https://pulsex.mypinata.cloud/ipfs/bafybeidea3ibq4lu5t6vk6ihp4iuznjb3ltsdm5y2shv4atxgyd3d33aim/#/?outputCurrency=0x1c2766F5949A4aA5d4cf0439067051135ffc1b28',
		explorer: 'https://scan.dextop.pro/#/token/0x1c2766F5949A4aA5d4cf0439067051135ffc1b28?tab=contract',
		git: ''
	};
	import { Github, Send, Twitter } from "lucide-svelte";

</script>



<footer class={footStyle}>
	<div class="flex flex-col container items-center">
		<a href="/" class="inline-flex items-center">
			<img src={rob} alt="ROB" class="h-10" />
		</a>
		<div class="flex flex-row gap-2 text-lg">
			<a class="font-bold tracking-wide uppercase drop-shadow" target="_blank" href={link.swap}>buy on PulseX</a
			>
			|
			<a class="font-bold tracking-wide uppercase drop-shadow" target="_blank" href={link.explorer}>contract</a>
		</div>
		<span class="block text-sm text-center">
			
			<a
				style="color: #eab308;"
				href="https://x.com/search?q=%24rob&src=typed_query&f=live"
				class="hover:underline drop-shadow"
			>
				$ROB
			</a> | <a
				style="color: #eab308;"
				href="https://x.com/shaneheartwin"
				class="hover:underline drop-shadow"
			>@shaneheartwin
			</a>
		</span>
		<div>
			<div class="flex items-center gap-1 px-2">
				<a target="_blank" class="p-2 min-w-xl" href={link.xapp}>
					<Twitter size="20" />
				</a>
				<a target="_blank" href={link.tele} class="p-2 min-w-xl">
					<Send size="20" />
				</a>
				<a target="blank" class="p-2 min-w-xl" href={link.git}>
					<Github size="20" />
				</a>
			</div>
		</div>
	</div>
</footer>
