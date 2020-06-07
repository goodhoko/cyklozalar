<script>
  import { onMount } from 'svelte';
  import Head from '../components/Head.svelte'

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

<h1>Žalář</h1>
<section>
	<p>Nezávislá cyklodílna obnovená ze zbytků a přeživších bývalé Vinohradské dílny T9.</p>
	<p>Z Vinohradů jsme se přesunuli do Karlínských močálů, ale kola děláme furt stejná. Naším řemeslem jsou zakázkové stavby fixedgear, singlespeed a silniční bicyklů. V mezičase organizujeme vyjížďky a jiné sněmy Pražské cyklo komunity.</p>
</section>

<section>
	<div class="heads">
		<Head name='Jen' nameSlug='jen'/>
		<Head name='Matouš' nameSlug='matous'/>
		<Head name='Šimon' nameSlug='simon'/>
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
