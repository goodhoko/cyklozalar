<script>
    export let name, nameSlug;
    let email = `${nameSlug}@zalar.cc`;
</script>

<style>
    .head {
		display: flex;
		flex-direction: column;
		align-items: center;
        width: 33%;
	}

	.head img {
		border-radius: 50%;
		width: 50%;
	}

	.head .name {
		text-align: center;
		display: block;
	}

    @media (max-width: 800px) {
		.head {
			width: 50%;
		}
	}
</style>

<div class="head">
    <span class="name">{name}</span>
    <img src="/images/{nameSlug}.jpg" alt="{name} jede na kole">
    <a href="mailto:{email}">{email}</a>
</div>
