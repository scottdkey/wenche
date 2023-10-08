<script lang="ts">
	import wenche from '../images/wenche.png';
	const buttonClass = 'embedded-checkout-modal-checkout-button';

	function showCheckoutWindow(e: MouseEvent) {
		e.preventDefault();
		let element = document.getElementById(buttonClass);

		if (element) {
			const url = element.getAttribute('data-url');
			const title = 'Square Online Checkout';

			// Some platforms embed in an iframe, so we want to top window to calculate sizes correctly
			const topWindow = window.top ? window.top : window;

			// Fixes dual-screen position                                Most browsers          Firefox
			const dualScreenLeft =
				topWindow.screenLeft !== undefined ? topWindow.screenLeft : topWindow.screenX;
			const dualScreenTop =
				topWindow.screenTop !== undefined ? topWindow.screenTop : topWindow.screenY;

			const width = topWindow.innerWidth
				? topWindow.innerWidth
				: document.documentElement.clientWidth
				? document.documentElement.clientWidth
				: screen.width;
			const height = topWindow.innerHeight
				? topWindow.innerHeight
				: document.documentElement.clientHeight
				? document.documentElement.clientHeight
				: screen.height;

			const h = height * 0.75;
			const w = 500;

			const systemZoom = width / topWindow.screen.availWidth;
			const left = (width - w) / 2 / systemZoom + dualScreenLeft;
			const top = (height - h) / 2 / systemZoom + dualScreenTop;
			if (url) {
				const newWindow = window.open(
					url,
					title,
					`scrollbars=yes, width=${w / systemZoom}, height=${
						h / systemZoom
					}, top=${top}, left=${left}`
				);
				if (window && window.focus !== undefined && newWindow) newWindow.focus();
			}

			// This overrides the default checkout button click handler to show the embed modal
			// instead of opening a new tab with the given link url
			element.addEventListener('click', function (e) {
				showCheckoutWindow(e);
			});
		}
	}
</script>

<div class="main">
	<h1 class="header">Wenche Donation</h1>
	<img alt="Wenche Playing the flute" src={wenche} class="primaryPhoto" />
	<p class="paragraphText">
		Hvis du er her, er det en god sjangse for at Wenche har hjulpet deg på et tidspunkt, enten som
		lærer, kollega eller medmenneske. Men nå er det Wenche som trenger vår hjelp. I perioden
		mars/april 2023 ble hun svindlet av tre iranske menn, som påsto de trengte hjelp til å få sin
		mor ut av Iran. Som alltid var Wenche godhjertet og ville hjelpe, selv om disse mennene til
		tider opptredte truende. To av dem skaffet seg blandt annet adgang til leiligheten hennes, og
		presset henne til å «hjelpe» dem. Historien deres var ren fabrikasjon, og hun mistet alle
		sparepengene side – 45.000 Nok. Nå står Wenche i fare for å miste leiligheten sin, hvis hun ikke
		klarer nedbetalingene. Derfor trenger vi DIN hjelp – uansett hvor mye eller lite du har mulighet
		til å gi. Alle monner drar, og målet vårt er å overraske Wenche – derfor er det veldig viktig at
		ingen nevner dette for henne. Dette er også grunnen til at vi ikke bruker etternavnet hennes
		her. Vi har også satt målet til 48.000 pga at GoFundMe tar et gebyr per donasjon, slik at disse
		gebyrene ikke vil «spise» seg inn i de 45.000 Wenche trenger.
	</p>
	<div>
		<div>
			<div class="container">
				<div>
					<button
						type="button"
						on:click={(e) => {
							showCheckoutWindow(e);
							window.open('https://square.link/u/6jSZn1WE?src=embed', '_blank');
						}}
						class="button">Donate</button
					>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.main {
		height: 100vh;
		width: 100vw;
		margin: unset;
		padding: unset;
		position: absolute;
		background: rgb(14, 12, 40);
		background: linear-gradient(
			156deg,
			rgba(14, 12, 40, 1) 0%,
			rgba(68, 120, 81, 1) 33%,
			rgba(0, 193, 255, 0.9081632653061225) 100%
		);
	}
	.header {
		background-color: rgba(250, 235, 215, 0.553);
		width: fit-content;
		padding-left: 5px;
		padding-right: 10px;
		border-radius: 10px;
		margin-left: 40px;
		box-shadow: 5px 5px 10px #00000079;
	}
	.container {
		margin-left: auto;
		margin-right: auto;
		overflow: auto;
		display: flex;
		flex-direction: column;
		justify-content: flex-end;
		align-items: center;
		width: fit-content;
		background: rgba(250, 235, 215, 0.553);
		padding: 7px;
		border: 1px solid rgba(0, 0, 0, 0.1);
		border-radius: 10px;
	}
	.button {
		display: inline-block;
		font-size: 18px;
		line-height: 48px;
		height: 48px;
		color: #ffffff;
		border-radius: 10px;
		min-width: 200px;
		background-color: #0b4972;
		text-align: center;
		transition: ease-in-out 0.1s;
		&:hover {
			background-color: #0f0f9383;
		}
	}
	.paragraphText {
		margin-left: auto;
		margin-right: auto;
		max-width: 80%;
		background-color: rgba(250, 235, 215, 0.513);
		padding: 10px;
		border-radius: 10px;
	}
	.primaryPhoto {
		display: block;
		margin-left: auto;
		margin-right: auto;
		max-height: 20em;
		border-radius: 10px;
		box-shadow: 1px 1px 2em #00000079;
	}
</style>
