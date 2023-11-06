<script>
	import { page } from "$app/stores";
	import logo from "$lib/images/favicon.png";
	import { ethers } from "ethers";
	import { browser } from "$app/environment";
	import { onMount } from "svelte";

	let provider;
	let wallet;
	let signer;

	onMount(async () => {
		if(browser) {

		}
	}); 

	async function loginWithMetaMask() {
		try {
			provider = new ethers.BrowserProvider(window.ethereum);
			signer = await provider.getSigner();
			wallet = (signer.address).toString();
			formatAddress();
		} catch (error) {
			console.error("MetaMask login failed:", error);
		}
	}

	function formatAddress() {
		wallet = wallet.slice(0, 4) + "..." + wallet.slice(wallet.length - 4, wallet.length);
	}


</script>

<header>
	<div class="corner left">
		<div>
			<img src={logo} alt="StopBlock"/>
		</div>
	</div>

	<nav>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L1,2 C1.5,3 1.5,3 2,3 L2,0 Z" />
		</svg>
		<ul>
			<li aria-current={$page.url.pathname === "/" ? "page" : undefined}>
				<a href="/">Game</a>
			</li>
			<li aria-current={$page.url.pathname === "/info" ? "page" : undefined}>
				<a href="/info">Info</a>
			</li>
		</ul>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
		</svg>
	</nav>

	<div class="corner right">
		{#if provider == null || provider == undefined}
		<button class="login" on:click={loginWithMetaMask}>Login</button>
		{:else}
		<button class="logout">{wallet}</button>
		{/if}
	</div>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
	}

	.corner {
		width: 50%;
		height: 3em;
	}

	.corner img {
		width: 50px;
		height: 50px;
		object-fit: contain;
	}

	.left {
		display: grid;
		justify-items: left;
		padding: 5px 0px 0px 5px;
	}

	.right {
		display: grid;
		justify-items: right;
		padding: 5px 5px 0px 0px;
	}

	nav {
		display: flex;
		justify-content: center;
		--background: #644dff;
	}

	svg {
		width: 2em;
		height: 3em;
		display: block;
	}

	path {
		fill: #644dff;
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: #644dff;
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
	}

	li[aria-current="page"]::before {
		--size: 6px;
		content: "";
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid #1a1829;
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 0.5rem;
		color: var(--color-text);
		font-weight: 700;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: #2f2f35;
	}

	.login {
		color: #ffffff;
		font-size: 20px;
		width: 118px;
		background-color: #644dff;
		border-radius: 8px;
		margin: 0px;
		padding: 0px 5px;
		border: 2px solid #b9aeff;
		cursor: pointer;
	}

	.logout {
		color: #ffffff;
		font-size: 18px;
		width: 118px;
		background-color: #644dff;
		border-radius: 8px;
		margin: 0px;
		padding: 0px 5px;
		border: 2px solid #b9aeff;
		cursor: pointer;
	}
</style>
