<script context="module" lang="ts">
	export const prerender = true;
</script>

<svelte:head>
	<title>V/A Player</title>
</svelte:head>

<section>
	<div class="form">
		<h1>Just Entering Your Link:</h1>
		<form action="/link/" class="linkForm">
			<input type="text" placeholder="ur link" name="link">
			<br>
			<button type="submit">GoGo~</button>
		</form>

		<div class="subtext">
			
		</div>
	</div>
</section>

<footer>
	&copy; Copyright 2022 <a sveltekit:prefetch href="https://suphakit.net/">Suphakit P.</a> All right reserved.
</footer>
	
<style>
	section {
		width: 100%;
		height: 100vh;
		
		display: flex !important;
		justify-content: center;
		vertical-align: middle;
		align-items: center;

		color: whitesmoke;
	}

	.form {
		height: auto;
		width: 100%;
		text-align: center;
	}
	
	.linkForm {
		width: 100%;
		text-align: center;
	}

	.linkForm input {
		width: 69.60%;
		text-align: center;

		border: none;
		border-radius: 0;
		border-top-left-radius: 10px;
		border-top-right-radius: 10px;

		padding-top: 1rem;
		padding-bottom: 1rem;
		
		font-size: 20px;
	}

	.linkForm button {
		width: 70%;

		padding-top: 1rem;
		padding-bottom: 1rem;

		border: none;
		border-radius: 0;
		border-bottom-left-radius: 10px;
		border-bottom-right-radius: 10px;

		background-color: coral;
		color: whitesmoke;
		font-size: 20px;

		transition: .3s;
	}

	.linkForm button:hover {
		cursor: pointer;
		opacity: 0.8;
	}

	footer {
		width: 100%;

		position: fixed;
		bottom: 0;

		text-align: center;

		padding: 1rem;

		background-color: whitesmoke;
		color: #2e2f2f;
	}

	footer a {
		color: #2e2f2f;
		text-decoration: none;
	}

	footer a:hover {
		color: #2e2f2f;
		text-decoration: underline;
	}
</style>