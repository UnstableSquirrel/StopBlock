<script>
	import morty from "$lib/images/son.jpg";
	import both from "$lib/images/both.jpg";
</script>


<svelte:head>
	<title>Info</title>
	<meta name="description" content="Information" />
</svelte:head>

<div class="text-column">
	<h1>What is StopBlock?</h1>

	<p>
	   StopBlock is a smart contract inspired by the War of Attrition Game Theory and by the Fomo3d contract of 2018.
	   It is a new form of contract without the need for a ERC20 token or a Uniswap pool. It deosn't need redeployment
	   when starting a new game round and has a built in algorithm to automatically calculate ticket prizes aswell as
	   distribution of reflections.
	</p>

	<br>

	<h3>How does it work?</h3>
	<p>
		It is pretty simple, you buy a ticket in order to win the prize, and you get reflections for each ticket bought.
	</p>

	<br>

	<h3>How?</h3>
	<p>Each ticket bought goes into a ETH pool and is distributed amongst the winner and the ticket buyers at the end.</p>

	<br>

	<h3>How much, anon?</h3>
	<p>
	   50% of the total pool funds go the the winner, 
	   45% goes back to the players who bought tickets as reflections, 
	   5% goes to the dev wallet.
	</p>

	<img src="{morty}" alt="You son of a bitch, I'm in!">
	<br>
	<br>

	<br>

	<h3>Tell me more ...</h3>
	<p>		
		Each ticket buy adds 10 blocks to a count down timer, and also increases the prize of the next ticket by 0.001 ETH.
	</p>

	<br>

	<h3>Buy early, or later on</h3>
	<p>
		You can get in early and benefit from the low ticket prizes through reflections, or get in at a later point with a
		good chance to be the last buyer and win the main prize.
	</p>

	<img src="{both}" alt="Why not both?">
	<br>
	<br>

	<br>
	<br>

	<h3>If you're still there, here is a simple breakdown of the core game mechanics:</h3>

	<p>&#10687 Buy ticket for ETH</p>

	<p>&#10687 Increase the block timer by 10 for each ticket bought</p>

	<p>&#10687 Each ticket buy also increases the ticket prize by 0.001 ETH</p>

	<p>&#10687 Last buying address when the timer runs out wins 50% of the total pool</p>

	<p>&#10687 45% of the pool will be claimable for all ticket buyers after each round</p>

	<br>
	<br>

	<h3>And here are the contract informations:</h3>

	<p>&#10687 Contract: <strong>TBA</strong></p>

	<p>&#10687 Tax: <strong>0%</strong></p>

	<p>&#10687 Max <strong>255 tickets</strong> per transaction</p>

	<p>&#10687 Starting Price: <strong>0.001 ETH</strong></p>

	<p>&#10687 Price increase per transaction: <strong>0.001 ETH</strong></p>

	<br>
	<br>
	<br>


	<h3>Don't need more info, anon. You already had me at 'reflections'.</h3>


	<br>
	<br>
	<br>

</div>

<style>
	img {
		max-width: 400px;
		width: 100%;
		height: auto;
	}
</style>
