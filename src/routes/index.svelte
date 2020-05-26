<script>
  import { onMount } from 'svelte';

  onMount(() => {
    if (window.netlifyIdentity) {
      window.netlifyIdentity.on("init", user => {
        if (!user) {
          window.netlifyIdentity.on("login", () => {
            document.location.href = "/admin/";
          });
        }
      });
    }
  });
</script>

<style>
	h1, figure, p {
		text-align: center;
		margin: 0 auto;
	}

	h1 {
		font-size: 2.8em;
		font-family: 'Jim Nightshade', cursive;
		text-transform: uppercase;
		font-weight: 700;
		margin: 0 0 0.5em 0;
	}

	figure {
		margin: 0 0 1em 0;
	}

	img {
		width: 100%;
		max-width: 400px;
		margin: 0 0 1em 0;
	}

	p {
		margin: 1em auto;
	}

	@media (min-width: 480px) {
		h1 {
			font-size: 4em;
		}
	}
</style>

<svelte:head>
	<title>Žalář ⫵⫵⫵ Cyklodílna</title>
	<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
</svelte:head>

<h1>Žalář ⫵⫵⫵</h1>
<p>Nezávislá cyklodílna obnovená ze zbytků a přeživších bývalé Vinohradské dílny T9.</p>
<p>Z Vinohradů jsme se přesunuli do Karlínských močálů, ale kola děláme furt stejná. Naším řemeslem jsou zakázkové stavby fixedgear, singlespeed a silniční bicyklů. V mezičase organizujeme vyjížďky s jiné sněmy Pražské cyklo komunity.</p>

<h2>Pikající</h2>
<div class="heads">
	<div>
		<h3>Honza</h3>
		<img src="/heads/honza.jpg" alt="Portrét Honzy">
		<a href="mailto:jen@zalar.cc">jen@zalar.cc</a>
	</div>
	<div>
		<h3>Matouš</h3>
		<img src="/heads/matous.jpg" alt="Portrét Matouše">
		<a href="mailto:jen@zalar.cc">matous@zalar.cc</a>
	</div>
	<div>
		<h3>Šimon</h3>
		<img src="/heads/simon.jpg" alt="Portrét Šimona">
		<a href="mailto:jen@zalar.cc">simon@zalar.cc</a>
	</div>
</div>

<h2>Projekty</h2>
<div class="projects-sample">

	<a href="/projekty">všechny projekty</a>
</div>
