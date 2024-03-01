<script>
	import * as Tabs from '$lib/components/ui/tabs';
	import * as Card from '$lib/components/ui/card';
	import * as AlertDialog from '$lib/components/ui/alert-dialog';
	import { Button } from '$lib/components/ui/button';
	import { Input } from '$lib/components/ui/input';
	import { Label } from '$lib/components/ui/label';
	import {
		tokensEarned,
		tokenBalance,
		tokensStaked,
		lpTokenBalance,
		tokenEmissionPerSec
	} from './(components)/contractData';
	import StakeTokens from './(components)/StakeTokens.svelte';
	import GetContractData from './(components)/GetContractData.svelte';
	import ClaimRewards from './(components)/ClaimRewards.svelte';
	import ApproveTokens from './(components)/ApproveTokens.svelte';
	import WithdrawTokens from './(components)/WithdrawTokens.svelte';
	import { ExternalLink } from 'radix-icons-svelte';
	import { Separator } from "$lib/components/ui/separator";
	import { ethers } from 'ethers';
	import { BigNumber } from 'bignumber.js';
	import {
	Plus,
	Minus
  } from "lucide-svelte";
  	import leancircle from "$lib/images/leancircle.png";
	import pls from "$lib/images/pls.png";
	import inc from "$lib/images/inc.png";
	import rob from "$lib/images/rob.png";
	import plsx from "$lib/images/plsx.png";

	let earnedTokens;
	let stakedLean;
	let leanBalance;
	let lpBalance;
	let emissionsPerDay;

	tokensEarned.subscribe((earned) => {
		earnedTokens = earned;
	});
	tokensStaked.subscribe((tokens) => {
		stakedLean = tokens;
	});
	tokenBalance.subscribe((tokens) => {
		leanBalance = tokens;
	});
	lpTokenBalance.subscribe((tokens) => {
		lpBalance = tokens;
	});
	tokenEmissionPerSec.subscribe((tokens) => {
		emissionsPerDay = (Number(tokens) * 86400);
	})


	const title =
		'font-bebas-neue uppercase text-4xl font-black flex flex-col container leading-none';

	const LinkIcon = '<svg width="15" height="15" viewBox="0 0 15 15" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M3 2C2.44772 2 2 2.44772 2 3V12C2 12.5523 2.44772 13 3 13H12C12.5523 13 13 12.5523 13 12V8.5C13 8.22386 12.7761 8 12.5 8C12.2239 8 12 8.22386 12 8.5V12H3V3L6.5 3C6.77614 3 7 2.77614 7 2.5C7 2.22386 6.77614 2 6.5 2H3ZM12.8536 2.14645C12.9015 2.19439 12.9377 2.24964 12.9621 2.30861C12.9861 2.36669 12.9996 2.4303 13 2.497L13 2.5V2.50049V5.5C13 5.77614 12.7761 6 12.5 6C12.2239 6 12 5.77614 12 5.5V3.70711L6.85355 8.85355C6.65829 9.04882 6.34171 9.04882 6.14645 8.85355C5.95118 8.65829 5.95118 8.34171 6.14645 8.14645L11.2929 3H9.5C9.22386 3 9 2.77614 9 2.5C9 2.22386 9.22386 2 9.5 2H12.4999H12.5C12.5678 2 12.6324 2.01349 12.6914 2.03794C12.7504 2.06234 12.8056 2.09851 12.8536 2.14645Z" fill="currentColor" fill-rule="evenodd" clip-rule="evenodd"></path></svg>';
</script>
<GetContractData />
<div style="background-color: --background;" class='relative flex flex-col items-center'>
	<div class="h-10" />
	<h1 class={title}>
		<span
			class="text-6xl text-transparent bg-clip-text bg-gradient-to-r from-yellow-500 to-amber-400"
			>Farms</span
		>Stake ROB & earn yield.
	</h1>
	<div class="h-10 h-10" />
	<Tabs.Root value="pools" class="w-96 mb-10">
		<Tabs.List class="grid w-full grid-cols-2 ">
			<Tabs.Trigger value="pools">Pools</Tabs.Trigger>
			<Tabs.Trigger value="earn">Earn ROB 🥇</Tabs.Trigger>
			
		</Tabs.List>
		<Tabs.Content value="earn">
			<Card.Root class="backdrop-blur w-96">
				<Card.Header class="p-5">
					<h1 class="text-3xl font-bold">Stake</h1>
					<Card.Title><strong>ROB-WPLS LP</strong> & earn <strong>ROB 🥇</strong></Card.Title>
				</Card.Header>
				<Card.Content>
					<Card.Description>

						<!-- {#if account.isConnected}
							<GetContractData />
							<script>
								console.log();("true");
							</script>
						{/if} -->
						
						<div class="flex flex-row">
							<div class="flex justify-center flex-col font-dm text-sm font-medium">
								<p class="px-2">ROB Earned:<br />{earnedTokens}</p>
								<p class="px-2">ROB/WPLS LP Staked:<br />{stakedLean}</p>
								<p class="px-2">ROB Balance:<br />{leanBalance}</p>
								<p class="px-2">LP Balance:<br />{lpBalance}</p>
								<!-- <p class="px-2">50000000</p> total -->
								<!-- <Progress value={earnedTokens} max={50000000} /> -->
								<!-- <div style="justify-content:space-between;" class="flex">
									<p>0</p>
									<p>100,000,000</p>
								</div> -->
								<p class="px-2">Daily Distribution:<br />0.0 ROB</p>
							</div>
							<div class="flex flex-col font-dm text-sm font-medium">
								<p class="px-2">Finished</p>
							</div>
						</div>
					</Card.Description>
				</Card.Content>
				<div style="justify-content: space-between;" class="px-6 flex flex-row">
					<span style="text-decoration: underline;" class="flex flex pb-3">
						<div></div>
						<a
							style="font-size: 12px;"
							href="https://bafybeicjuszlj6w3gg5mfszvo7z6ux4iaafhw62vfyfw27nm65bexodov4.ipfs.dweb.link/#/address/0x1c2766F5949A4aA5d4cf0439067051135ffc1b28"
							target="_blank">View Contract
						</a>
							<ExternalLink size={10} />
							<!-- <Separator orientation="vertical" class="" /> -->
					</span>
					<span style="text-decoration: underline;" class="flex flex pb-3">
							<a
							style="font-size: 12px;"
							href="https://bafybeihiwe3inbfru7h6pesaj4siacbyx7t6o5qp3vwdz25n3p6ewlbnie.ipfs.dweb.link/#/add/V2/PLS/0x1c2766F5949A4aA5d4cf0439067051135ffc1b28"
							target="_blank">Add Liquidity
						</a>
							<ExternalLink size={10} />
					</span>
					<span style="text-decoration: underline;" class="flex flex pb-3">
						<a
						style="font-size: 12px;"
						href="https://bafybeihiwe3inbfru7h6pesaj4siacbyx7t6o5qp3vwdz25n3p6ewlbnie.ipfs.dweb.link/#/?outputCurrency=0x1c2766F5949A4aA5d4cf0439067051135ffc1b28"
						target="_blank">Trade ROB
					</a>
						<ExternalLink size={10} />
					</span>
				</div>
				
				
				

				<Card.Footer class="space-x-3 flex justify-center p-4">
					<ApproveTokens />
					<ClaimRewards />

					<AlertDialog.Root>
						<AlertDialog.Trigger asChild let:builder>
							<Button disabled class="hover:bg-gray-700" builders={[builder]}>Stake</Button>
						</AlertDialog.Trigger>
						<AlertDialog.Content>
							<AlertDialog.Header>
								<AlertDialog.Title>Stake ROB/WPLS LP 🥇</AlertDialog.Title>
								<!-- <AlertDialog.Description>
										How many tokens do you want to stake?
									</AlertDialog.Description> -->
							</AlertDialog.Header>

							<AlertDialog.Footer>
								<StakeTokens />
								<!-- <Input type="email" placeholder="Amount" />
									<AlertDialog.Action>Claim</AlertDialog.Action>
									<AlertDialog.Cancel>Cancel</AlertDialog.Cancel> -->
							</AlertDialog.Footer>
						</AlertDialog.Content>
					</AlertDialog.Root>

					<AlertDialog.Root>
						<AlertDialog.Trigger asChild let:builder>
							<Button class="hover:bg-gray-700" builders={[builder]}>Withdraw</Button>
						</AlertDialog.Trigger>
						<AlertDialog.Content>
							<AlertDialog.Header>
								<AlertDialog.Title>Withdraw ROB/WPLS LP 🥇</AlertDialog.Title>
								<!-- <AlertDialog.Description>
																	How many tokens do you want to stake?
																</AlertDialog.Description> -->
							</AlertDialog.Header>

							<AlertDialog.Footer>
								<WithdrawTokens />
								<!-- <Input type="email" placeholder="Amount" />
																<AlertDialog.Action>Claim</AlertDialog.Action>
																<AlertDialog.Cancel>Cancel</AlertDialog.Cancel> -->
							</AlertDialog.Footer>
						</AlertDialog.Content>
					</AlertDialog.Root>
					
				</Card.Footer>
			</Card.Root>
		</Tabs.Content>
		<Tabs.Content value="pools"> 
			<Card.Root class="backdrop-blur w-96">
				<Card.Header class="p-5">
					<h1 class="text-3xl font-bold">ROB Pools</h1>
					<Card.Title><code>Stake LP & earn ????</code></Card.Title>
				</Card.Header>
				<Card.Content class="py-0 text-center">
					<div class="flex justify-between mb-2">
						<div class="bg-gradient-to-t from-white/5 to-white/15 rounded-sm py-3 px-2 w-full text-right px-3">

							<div style="transform: translate(0, 10px)">
								
								<img style="position: absolute; transform: translate(0px, 0px);" src={rob} alt="ROB" width="48">
								<img style="position: absolute; transform: translate(0px, 0px);" src={plsx} alt="PLSX" width="20">
							</div>
								
								<p>Stake <strong>ROB-PLSX</strong> Earn ????</p>
							
							<Button class="p-2"><Plus /></Button>
							<Button class="p-2"><Minus /></Button>
						</div>
						
					</div>

					<div class="flex justify-between mb-2">
						<div class="bg-gradient-to-t from-white/5 to-white/15 rounded-sm py-3 px-2 w-full text-right px-3">

							<div style="transform: translate(0, 10px)">
								
								<img style="position: absolute; transform: translate(0px, 0px);" src={rob} alt="ROB" width="48">
								<img style="position: absolute; transform: translate(0px, 0px);" src={inc} alt="INC" width="20">
							</div>
								
								<p>Stake <strong>ROB-INC</strong> Earn ????</p>
							
							<Button class="p-2"><Plus /></Button>
							<Button class="p-2"><Minus /></Button>
						</div>
						
					</div>

					<div class="flex justify-between mb-2">
						<div class="bg-gradient-to-t from-white/5 to-white/15 rounded-sm py-3 px-2 w-full text-right px-3">

							<div style="transform: translate(0, 10px)">
								
								<img style="position: absolute; transform: translate(0px, 0px);" src={rob} alt="ROB" width="48">
								<img style="position: absolute; transform: translate(0px, 0px);" src={leancircle} alt="LEAN" width="20">
							</div>
								
								<p>Stake <strong>ROB-LEAN</strong> Earn ????</p>
							
							<Button class="p-2"><Plus /></Button>
							<Button class="p-2"><Minus /></Button>
						</div>
						
					</div>
					
				</Card.Content>

				<div style="justify-content: space-between;" class="px-6 py-2 flex flex-row">
					<span style="text-decoration: underline;" class="flex flex pb-3">
						<div></div>
						<a
							style="font-size: 12px;"
							href="https://bafybeicjuszlj6w3gg5mfszvo7z6ux4iaafhw62vfyfw27nm65bexodov4.ipfs.dweb.link/#/address/0x1c2766F5949A4aA5d4cf0439067051135ffc1b28"
							target="_blank">View Contract
						</a>
							<ExternalLink size={10} />
							<!-- <Separator orientation="vertical" class="" /> -->
					</span>
					<span style="text-decoration: underline;" class="flex flex pb-3">
							<a
							style="font-size: 12px;"
							href="https://bafybeihiwe3inbfru7h6pesaj4siacbyx7t6o5qp3vwdz25n3p6ewlbnie.ipfs.dweb.link/#/add/V2/PLS/0x1c2766F5949A4aA5d4cf0439067051135ffc1b28"
							target="_blank">Add Liquidity
						</a>
							<ExternalLink size={10} />
					</span>
					<span style="text-decoration: underline;" class="flex flex pb-3">
						<a
						style="font-size: 12px;"
						href="https://bafybeihiwe3inbfru7h6pesaj4siacbyx7t6o5qp3vwdz25n3p6ewlbnie.ipfs.dweb.link/#/?outputCurrency=0x1c2766F5949A4aA5d4cf0439067051135ffc1b28"
						target="_blank">Trade ROB
					</a>
						<ExternalLink size={10} />
					</span>
				</div>

				<Card.Footer class="p-0 flex justify-center">
					<!-- <ApproveTokens />
					<ClaimRewards /> -->

					
				</Card.Footer>
			</Card.Root>
		</Tabs.Content>
	</Tabs.Root>
	
	<!-- <div style="justify-content: center;" class="flex"> -->
		<!-- <Button
			target="_blank"
			href="https://app.pulsex.com/swap?outputCurrency=0x1c9b5e57AA89f8b58CA28249E347A6C933726449"
			style="line-height: 1.2; width: 12em; margin-top: 0.5em;"
			class="transition-colors justify-center block shadow-lg text-base text-white hover:text-gray-100 bg-green-500 hover:bg-green-300 hover:backdrop-blur-xl backdrop-blur-lg rounded-md"
		>
			BUY $LEAN
		</Button> -->
		<!-- <button
						style="margin: 10px;"
						class="block shadow-lg px-8 py-3 text-base font-medium text-gray-200 hover:text-gray-100 bg-gray-100/10 hover:bg-gray-200/30 hover:backdrop-blur-xl backdrop-blur-lg rounded-md md:py-4 md:text-lg md:px-8"
					>
						Learn More
					</button> -->
	<!-- </div> -->
</div>


<style>
	.video-docker::after {
		content: '';
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		z-index: 1;
	}
</style>
