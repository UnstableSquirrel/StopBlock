<script>
	import { spring } from "svelte/motion";

	let count = 0;
	const displayed_count = spring();
	$: displayed_count.set(count);
	$: offset = modulo($displayed_count, 1);

	let walletAddress = "0x0000000000000000000000000000000000000000";

	function formatAddress() {
		walletAddress = walletAddress.slice(0, 4) + "..." + walletAddress.slice(walletAddress.length - 4, walletAddress.length);
	}
	formatAddress();

	function modulo(n, m) {
		// handle negative numbers
		return ((n % m) + m) % m;
	}

	function timer() {
		setTimeout((() => {
			count++;
			timer();
		}), 1000);
	}
	// timer();

	let ticketsSold = 0;
	let tickets = 1;
	let prizePool = "0.00"
	let claimable = "0.00"
	let ticketsPrize = 0.001;
	let paid = 0;

	function increment() {
		if(tickets < 255) {
			tickets = tickets + 1;
			calcPrize();
		}
	}

	function decrement() {
		if(tickets >= 2) {
			tickets = tickets - 1;
			calcPrize();
		}
	}

	let price_increase = 1 * 10 ** -3;
	function calcPrize() {
		let total = ticketsSold + tickets;
		ticketsPrize = ((total ** 2) + total) / 2;
		ticketsPrize = ((ticketsPrize * price_increase) - paid).toFixed(3);
	}

</script>

<svelte:head>
	<title>Game</title>
	<meta name="description" content="StopBlock main game" />
</svelte:head>

<section>
	<h1>StopBlock</h1>

	<div class="prize-container">
		<p>Current Prize:</p>
		<h3>{prizePool} ETH</h3>
	</div>

	<div class="main-box">
		<div class="counter">
			<h3>Blocks Left</h3>
			<div class="counter-viewport">
				<div class="counter-digits" style="transform: translate(0, {100 * offset}%)">
					<strong class="hidden" aria-hidden="true">{Math.floor($displayed_count + 1)}</strong>
					<strong>{Math.floor($displayed_count)}</strong>
				</div>
			</div>
		</div>
		
		<p style="margin: 0px;">00:00:00</p>

		<div class="ticket-cost-container">
			<p>Ticket Price:</p>
			<h3>{ticketsPrize} ETH</h3>
		</div>

		<div class="buttons-container">
			<div>
				<button class="btn ticket">Buy Ticket</button>
				<div class="ticket-amount-container">
					<button on:click={decrement}>-</button>
					<p style="font-size: 20px; font-weight: 700">{tickets}</p>
					<button on:click={increment}>+</button>
				</div>
			</div>
		</div>
	</div>

	<div class="buttons-container">
		<div>
			<button class="btn reward">Claim ETH</button>
			<p><span style="font-size: 17px; font-weight: 700">{claimable}</span> ETH Claimable</p>
		</div>	
	</div>

	<div class="last-buyer-container">
		<p>Last Buyer:</p>
		<a href="/"><strong>{walletAddress}</strong></a>
	</div>

</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		text-align: center;
		width: 100%;
		margin: 0px 0px 100px 0px;
		--😀: #644dff;
		--😀😀: #4836bb;
		--😀😀😀: #654dff63;
		font-size: 50px;
		font-weight: 800;
		letter-spacing: 2px;
		color: #ffffff;
		transform: skew(-10deg);
		transition: all .1s ease;
		z-index: 1;
	}

	p {
		margin: 5px;
	}

	.prize-container {
		display: grid;
		align-items: center;
		justify-items: center;
		grid-template-columns: auto auto;
		gap: 0px 5px;
		z-index: 1;
	}

	.prize-container > p {
		color: #e4e4e4;
	}

	.prize-container > h3 {
		color: white;
	}

	.main-box {
		background-color: #2f1b3d;
		width: 300px;
		height: 400px;
		padding: 15px;
		border-radius: 10px;
		display: flex;
		flex-direction: column;
		align-items: center;
		position: relative;
		backdrop-filter: blur(20px);
		text-align: center;
		border: 1px solid #fff;
		--rotate-animation: rotate(45deg);
		--scale-animation: scale(0);
	}

	.main-box::before {
		content: "";
		height: 110%;
		width: 110%;
		position: absolute;
		top: -5%;
		left: -5%;
		z-index: -1;
		background: linear-gradient(
			to right,
			#0f0c29,
			#302b63,
			#24243e
		);
		filter: blur(30px);
	}

	.ticket-cost-container {
		display: grid;
		align-items: center;
		justify-items: center;
		margin: 50px 0px 0px 0px;
	}

	.ticket-cost-container > p {
		color: #e4e4e4;
		margin: 0px;
	}

	.ticket-cost-container > h3 {
		margin: 10px 0px 0px 0px;
	}










/****************** Counter **********************************************************/
	.counter {
		display: flex;
		border-top: 2px solid #644dff;
		border-bottom: 2px solid #644dff;
		margin: 1rem 0;
	}

	.counter  > h3{
		color: rgb(216, 216, 216)	}

	.counter-viewport {
		width: 8em;
		height: 4em;
		overflow: hidden;
		text-align: center;
		position: relative;
	}

	.counter-viewport strong {
		position: absolute;
		display: flex;
		width: 100%;
		height: 100%;
		font-weight: 400;
		color: var(--color-theme-1);
		font-size: 45px;
		align-items: center;
		justify-content: center;
	}

	.counter-digits {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.hidden {
		top: -100%;
		user-select: none;
	}
/**********************************************************************************/










/****************** Button **********************************************************/
	.buttons-container {
		display: grid;
		align-items: center;
		justify-items: center;
		grid-template-columns: auto auto;
		margin-top: 50px;
		/* gap: 0px 50px; */
	}

	.buttons-container  > div {
		display: grid;
		align-items: center;
		justify-items: center;
		gap: 20px 0px;
	}

	.btn {
		--😀: #644dff;
		--😀😀: #4836bb;
		--😀😀😀: #654dff63;
		margin: 0px 0px 0px 0px;
		cursor: pointer;
		width: 184px;
		height: 48px;
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 1rem;
		font-size: 1.125em;
		font-weight: 800;
		letter-spacing: 2px;
		color: #fff;
		background: var(--😀);
		border: 2px solid var(--😀😀);
		border-radius: .75rem;
		box-shadow: 0 8px 0 var(--😀😀);
		transform: skew(-10deg);
		transition: all .1s ease;
		filter: drop-shadow(0 15px 20px var(--😀😀😀));
	}

	.btn:active {
		letter-spacing: 0px;
		transform: skew(-10deg) translateY(8px);
		box-shadow: 0 0 0 var(--😀😀😀);
	}
/**********************************************************************************/










	.ticket {
		margin: 0px 0px 0px 0px;
	}

	.reward {
		margin: 0px 0px 0px 0px;
		background: var(--😀);
		filter: drop-shadow(0 15px 20px var(--😀😀😀));
		border: 2px solid var(--😀😀);
		box-shadow: 0 8px 0 var(--😀😀);
	} 

	.buttons-container  > div > div {
		display: flex;
		margin: 0px 0px 0px 0px;
		gap: 0px 15px;
	}

	.ticket-amount-container {
		display: grid;
		align-items: center;
	}

	.ticket-amount-container > button {
		width: 50px;
		height: 30px;
		background-color: #9382ff;
		font-size: 20px;
		border-radius: 10px;
		border: 2px solid #4836bb;
		transition: all 0.2s linear;
		cursor: pointer;
		color: white;
	}

	.ticket-amount-container > button:hover {
		background-color: #c0b6ff;
	}

	.last-buyer-container {
		display: grid;
		justify-items: center;
		margin: 50px 0px 0px 0px;
		border-top: 2px solid #644dff;
		border-bottom: 2px solid #644dff;
		width: 100%;
	}

	.last-buyer-container > p {
		width: 100%;
		text-align: left;
		margin: 10px 0px 0px 0px;
		color: #e4e4e4;
	}

	.last-buyer-container > a {
		font-size: 20px;
		color: white;
		text-decoration: none;
		width: 100%;
		text-align: center;
		margin: 5px 0px 25px 0px;
		transition: all 0.2s linear;
	}

	.last-buyer-container > a:hover {
		color: #644dff;
	} 


</style>
