<script>
	import { onMount } from "svelte";
	import axios from "axios";

	let ip = "Loading...";

	let isCopy = false;

	onMount(async () => {
		await axios.get(https://api.ipify.org/?format=json)
		.then((res) => {
			ip = res.data.ip.toString()
		})
		.catch((err) => {
			ip = "Error"
		})
	})

	function copyIp() {
		var copyText = document.getElementById("ipInput");

		copyText.select();
		copyText.setSelectionRange(0, 99999);

		navigator.clipboard.writeText(copyText.value);

		isCopy = true

		setTimeout(() => {
			isCopy = false;
		}, 3000)
	}

</script>

<main>
	<div class="home">
		<a href="/" class="ip__heading">What's my IP?</a>

		<div class="ip__container">
			<input class="ip__input" value={ip} readonly id="ipInput">

			{#if !isCopy}
			<button class="ip__copy" on:click={copyIp}>
				
				<svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
				<path d="M14.0002 22H4.00019C3.46427 22.0186 2.94467 21.8139 2.56548 21.4347C2.1863 21.0555 1.98157 20.5359 2.00019 20V10C1.98157 9.46408 2.1863 8.94448 2.56548 8.5653C2.94467 8.18611 3.46427 7.98138 4.00019 8.00001H8.00019V4.00001C7.98157 3.46408 8.1863 2.94448 8.56548 2.5653C8.94467 2.18611 9.46427 1.98138 10.0002 2.00001H20.0002C20.5361 1.98138 21.0557 2.18611 21.4349 2.5653C21.8141 2.94448 22.0188 3.46408 22.0002 4.00001V14C22.0185 14.5358 21.8137 15.0553 21.4346 15.4344C21.0555 15.8135 20.536 16.0183 20.0002 16H16.0002V20C16.0185 20.5358 15.8137 21.0553 15.4346 21.4344C15.0555 21.8135 14.536 22.0183 14.0002 22ZM4.00019 10V20H14.0002V16H10.0002C9.46435 16.0183 8.94493 15.8135 8.56581 15.4344C8.18669 15.0553 7.98187 14.5358 8.00019 14V10H4.00019ZM10.0002 4.00001V14H20.0002V4.00001H10.0002Z" fill="#ffffff"></path>
				</svg>
			</button>

			{:else}

			<button class="ip__copy" on:click={copyIp}>
				<svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
				<path d="M9.52495 17.657L4.57495 12.707L5.98895 11.293L9.52645 14.8265L9.52495 14.828L18.01 6.343L19.424 7.757L10.939 16.243L9.52595 17.656L9.52495 17.657Z" fill="#ffffff"></path>
				</svg>
			</button>
			{/if}

		</div>
	</div>

	<span class="ip__v">IPv4</span>
</main>

<style>
	main {
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		background-color: #171717;
	}

	.home {
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.ip__heading {
		color: white;
		font-weight: 600;
		position: absolute;
		top: 30px;
		font-size: 18px;
		cursor: pointer;
		text-decoration: none;
	}

	.ip__v {
		position: absolute;
		bottom: 10px;
		right: 20px;
		color: gray;
		font-size: 14px;
		font-weight: 500;
		transition: 400ms;
		cursor: default;
	}

	.ip__v:hover {
		color: white;
	}

	.ip__container {
		display: flex;
		flex-direction: row;
	}

	.ip__input {
		width: 300px;
		height: 40px;
		padding-left: 10px;
		padding-right: 10px;
		background-color: #222222;
		border: 1px solid #333333;
		border-radius: 5px;
		outline: none;
		color: white;
		text-align: center;
		letter-spacing: 3px;
		font-weight: 600;
		font-size: 14px;
		margin-right: 5px;
		cursor: default;
	}

	.ip__input::selection {
		color: white;
		background: inherit;
	}

	.ip__copy {
		background-color: #222222;
		border: 1px solid #333333;
		border-radius: 5px;
		color: white;
		width: 50px;
		margin-left: 5px;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: 400ms;
	}

	.ip__copy:hover {
		border-color: gray;
	}

</style>
