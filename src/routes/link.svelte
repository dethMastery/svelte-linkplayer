<script context="module" lang="ts">
	export const prerender = true;
	import { onMount } from 'svelte';
</script>

<script lang='ts'>
	let link:any;
	let type:any;
	let fType:any;

	onMount(async() => {
		let call = new URLSearchParams(document.location.search);

		let get:any = call.get('link');
		link = get;
		console.log('link: ' + link);

		let typeGet = get.substr(get.length-3, get.length);		
		type = typeGet;
		console.log('file type: ' + type);
		
		if (type === 'wav') {
			fType = 'audio';
		} else if (type === 'mp3') {
			fType = 'audio';
		} else if (type === 'weba') {
			fType = 'audio';
		} else if (type === 'mp4') {
			fType = 'video';
		} else if (type === 'm4s') {
			fType = 'video';
		} else if (type === 'webm') {
			fType = 'video';
		} else {
			fType = 'other';
		}

		console.log('originType: ' + fType);
	});

	let duration:any;
	let muted:any = false;
	let currentTime:any = 0;
	let paused:any = false;
	let volume:any = 0.5;

	const format = (number: number) => {
		const minutes = Math.floor(number / 60);
		const secs = Math.floor(number % 60);
		
		return `${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
	}

	if (duration < 0) {
		duration = 0;
	}

	if (volume < 0) {
		volume = 0;
	} else if (volume > 1) {
		volume = 1;
	}

</script>

<svelte:head>
	<title>{type} | {link} | V/A Player</title>
</svelte:head>

<section>
	{#if fType === 'audio'}
		<div class="audio">
			<audio 
				src={link} 
				bind:duration={duration}		 
				bind:currentTime={currentTime}
				bind:muted={muted}
				bind:paused={paused}
				bind:volume={volume}

				autoplay
			>
			</audio>
			<div class="control">
				<div class="info">
					<h3>
						Link : {link}
					</h3>
					<h4>
						Type : {type}
					</h4>
					<progress
						value={currentTime}
						max={duration}
					/>
					<br>
					<span style="padding-bottom: 1rem;">
						{format(currentTime)} / {format(duration)}
					</span>
				</div>
				<div class="control-holder">
					<button class="back" on:click={e => currentTime = currentTime - 5}>
						-5
					</button>
					<button class="pp" on:click={e => paused = !paused}>
						Pause / Play
					</button>
					<button class="skip" on:click={e=> currentTime = currentTime + 5}>
						+5
					</button>
				</div>
				<div class="vControl">
					<span>volume</span>
					<br>
					<span>
						<button class="vDown" on:click={e => volume = volume - 0.1}>
							-
						</button>
						&nbsp;&nbsp;{Math.round(volume*100)}&nbsp;&nbsp;
						<button class="vUp" on:click={e => volume = volume + 0.1}>
							+
						</button>
					</span>
				</div>
			</div>
			<br />
			<div class="more">
				<span>More?</span>
				<form action="/link" method="get" class="again">
					<input type="text" placeholder="ur Link" name="link">
					<br>
					<button type="submit">
						gogo~
					</button>
				</form>
			</div>
		</div>
	{:else if fType === 'video'}
		<div class="video">
			<div class="control">
				<video 
					src={link} 
					bind:duration={duration}		 
					bind:currentTime={currentTime}
					bind:muted={muted}
					bind:paused={paused}
					bind:volume={volume}

					autoplay
				></video>
				<div class="info">
					<h4>
						Link : {link}
					</h4>
					<span class="subtext">
						Type : {type}
					</span>
					<progress
						value={currentTime}
						max={duration}
					/>
					<br>
					<span style="padding-bottom: 1rem;">
						{format(currentTime)} / {format(duration)}
					</span>
				</div>
				<div class="control-holder">
					<button class="back" on:click={e => currentTime = currentTime - 5}>
						-5
					</button>
					<button class="pp" on:click={e => paused = !paused}>
						Pause / Play
					</button>
					<button class="skip" on:click={e=> currentTime = currentTime + 5}>
						+5
					</button>
				</div>
				<div class="vControl">
					<span>volume</span>
					<br>
					<span>
						<button class="vDown" on:click={e => volume = volume - 0.1}>
							-
						</button>
						&nbsp;&nbsp;{Math.round(volume*100)}&nbsp;&nbsp;
						<button class="vUp" on:click={e => volume = volume + 0.1}>
							+
						</button>
					</span>
				</div>
			</div>
			<br />
			<div class="more" style="margin-bottom: 6rem;">
				<span>More?</span>
				<form action="/link" method="get" class="again">
					<input type="text" placeholder="ur Link" name="link">
					<br>
					<button type="submit">
						gogo~
					</button>
				</form>
			</div>
		</div>
	{:else}
		<div class="nothing">
			<h1>
				nothing
			</h1>
			<br>
			<a sveltekit:prefetch href="/">
				<button class="back">
					&lt; Go Back
				</button>
			</a>
		</div>
	{/if}
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

	.subtext {
		color: grey;
		font-size: 14px;
	}

	.audio, .video, .nothing {
		height: auto;
		text-align: center;
	}

	.video {
		display: flex !important;
		flex-direction: column;
		justify-content: center;
		align-content: center;
		align-items: center;
		text-align: center;
	}

	.control {
		width: 18rem;

		background-color: whitesmoke;
		color: #2e2f2f;

		border-radius: 10px;
		padding: 1rem;
	}

	.video .control {
		width: 70%;
		min-width: 18rem;
		padding: 0 !important;
	}

	.control video {
		width: 100%;
		border-top-left-radius: 10px;
		border-top-right-radius: 10px;
	}

	.control .info {
		/* padding-top: 1rem; */
		margin-bottom: 1rem;
	}

	.audio .control .info {
		width: auto;
		/* padding-top: 1rem; */
	}

	.control progress {
		width: 15rem;
		padding: 1rem;
		color: coral;
	}

	.control .control-holder {
		margin-bottom: 1rem;
	}

	.control .control-holder button {
		padding: 1rem;

		border: none;
		border-radius: 10px;

		background-color: coral;
		color: whitesmoke;

		transition: .3s;
	}

	.control .control-holder button:hover {
		opacity: 0.8;
		cursor: pointer;
	}

	.video .control .vControl {
		padding-bottom: 1rem;
	}

	.control .vControl button {
		width: 40px;
		height: 40px;

		border: none;
		border-radius: 50%;

		background-color: coral;
		color: whitesmoke;

		transition: .3s;
	}

	.control .vControl button:hover {
		opacity: 0.8;
		cursor: pointer;
	}

	.more .again {
		width: auto;
	}

	.more .again input {
		width: 13rem;
		height: auto;

		font-size: 15px;
		text-align: center;

		padding: .5rem;
		margin: 0;

		border: none;
		border-top-left-radius: 10px;
		border-top-right-radius: 10px;
	}

	.more .again button {
		width: 14rem;
		height: auto;

		font-size: 15px;
		color: whitesmoke;

		background-color: coral;
		padding: .35rem;
		margin: 0;

		border: none;
		border-bottom-left-radius: 10px;
		border-bottom-right-radius: 10px;

		transition: .3s;
	}

	.more .again button:hover {
		opacity: 0.8;
		cursor: pointer;
	}

	h1, h3, h4 {
		margin: 0;
		padding: 0;
	}

	.nothing .back {
		padding: 1rem;

		border: none;
		border-radius: 10px;

		background-color: coral;
		color: whitesmoke;
		font-size: 15px;
	}

	.nothing .back:hover {
		opacity: 0.8;
		cursor: pointer;
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
