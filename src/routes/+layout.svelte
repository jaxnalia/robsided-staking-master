<script>
	import "../app.pcss";

    import NavBar from '$lib/components/NavBar/NavBar.svelte';
    import FootBar from '$lib/components/FootBar/FootBar.svelte';
	import Analytics from '$lib/GAnalytics.svelte'
	import robleft from "$lib/images/robleft.png";
	import robright from "$lib/images/robright.png";
</script>

<svelte:head>
	<meta name="twitter:card" content="summary_large_image">
	<meta name="twitter:site" content="@shaneheartwin">
	<meta name="twitter:creator" content="@shaneheartwin">
	<meta name="twitter:title" content="ROB Sided Staking">
	<meta name="twitter:description" content="Stake ROB & Earn Yield.">
	<!-- <meta name="twitter:image" content="https://bigjax.s3.eu-west-2.amazonaws.com/twitter-image-2.jpg"> -->
	<meta property="og:title" content="ROB Sided Staking">
	<meta property="og:type" content="website">
	<!-- <meta property="og:url" content="https://leantoken.org/"> -->
	<!-- <meta property="og:image" content="https://bigjax.s3.eu-west-2.amazonaws.com/twitter-image-2.jpg"> -->
	<meta property="og:description" content="Stake ROB & Earn Yield.">
</svelte:head>
<Analytics />




<NavBar></NavBar>

<slot></slot>
<img style="position: absolute; left:0; transform: translateY(-73px); z-index: -1;" class="hidden sm:block" width="300" src={robleft} alt="robleft">


<img style="position: absolute; right:0; transform: translateY(-73px); z-index: -1;" width="300" src={robright} alt="robright">
<FootBar></FootBar>