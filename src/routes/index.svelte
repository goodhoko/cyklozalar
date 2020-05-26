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
	h1, p {
		text-align: center;
	}

	h1 {
		font-size: 2.8em;
		font-family: 'Jim Nightshade', cursive;
		margin: 0 0 0.5em 0;
	}
	section {
		padding-bottom: 3em;
	}

	p {
		margin: 1em auto;
	}

	.heads {
		display: flex;
		justify-content: center;
		flex-wrap: wrap;
	}

	.heads > div {
		width: 33%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.heads img {
		border-radius: 50%;
		width: 50%;
	}

	.heads .name {
		font-family: 'Jim Nightshade', cursive;
		text-align: center;
		display: block;
	}

	@media (min-width: 480px) {
		h1 {
			font-size: 4em;
		}
	}

	@media (max-width: 800px) {
		.heads > div {
			width: 50%;
		}
	}
</style>

<svelte:head>
	<title>Žalář ⫵⫵⫵ Cyklodílna</title>
	<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
</svelte:head>

<h1>Žalář</h1>
<section>
	<p>Nezávislá cyklodílna obnovená ze zbytků a přeživších bývalé Vinohradské dílny T9.</p>
	<p>Z Vinohradů jsme se přesunuli do Karlínských močálů, ale kola děláme furt stejná. Naším řemeslem jsou zakázkové stavby fixedgear, singlespeed a silniční bicyklů. V mezičase organizujeme vyjížďky a jiné sněmy Pražské cyklo komunity.</p>
</section>

<section>
	<div class="heads">
		<div>
			<span class="name">Jen</span>
			<img src="/images/jen.jpg" alt="Portrét Jena">
			<a href="mailto:jen@zalar.cc">jen@zalar.cc</a>
		</div>
		<div>
			<span class="name">Matouš</span>
			<img src="/images/matous.jpg" alt="Portrét Matouše">
			<a href="mailto:jen@zalar.cc">matous@zalar.cc</a>
		</div>
		<div>
			<span class="name">Šimon</span>
			<img src="/images/simon.jpg" alt="Portrét Šimona">
			<a href="mailto:jen@zalar.cc">simon@zalar.cc</a>
		</div>
	</div>
</section>

<h2>Projekty</h2>
<div class="projects-sample">
	<div class="project-tile">
		<a href="#s">Hello World!</a>
		<img src="content/images/p1010046.jpg" alt="hll wrld">
	</div>

	<a href="/projekty">všechny projekty</a>
</div>
