<script lang="ts">
	let editable = false;

	const toggleEditable = () => {
		editable = !editable;
	};

	let data: Record<string, null | HTMLElement> = {
		title: null,
		p1: null,
		p2: null,
		tab1: null,
		tab2: null,
	};

	$: {
		if (!editable) {
			Object.entries(data).forEach(([_, value]) => {
				console.log(value?.innerText);
			});
		}
	}
</script>

<div class="control">
	<button on:click={toggleEditable}>
		{#if editable}
			Save
		{:else}
			Edit
		{/if}
	</button>
</div>
<section class:edit={editable}>
	<h1 contenteditable={editable} bind:this={data.title}>Inline Editor</h1>

	<p contenteditable={editable} bind:this={data.p1}>
		Is he staying arrival address earnest. To preference considered it
		themselves inquietude collecting estimating.
	</p>

	<p contenteditable={editable} bind:this={data.p2}>
		Article nor prepare chicken you him now. Shy merits say advice ten
		before lovers innate add. She cordially behavior can attempted
		estimable. Trees delay fancy noise manor do as an small. Felicity now
		law securing breeding likewise extended and. Roused either who favour
		why ham.
	</p>

	<div class="tabs" contenteditable={editable}>
		<span class="tab" bind:this={data.tab1}>
			<h3>Always parish</h3>
			<p class="small">5 years of noise</p>
		</span>

		<span class="tab" bind:this={data.tab2}>
			<h3>Something parish</h3>
			<p class="small">10 years of some</p>
		</span>
	</div>
</section>

<style>
	.edit :is(h1, h3, p) {
		color: salmon;
	}

	section {
		display: grid;
		grid-template-columns: 1fr;
		grid-template-rows: auto;
		gap: 20px;
		padding: 3rem 0;
	}

	h1 {
		font-size: 3rem;
	}

	p {
		font-size: 1.25rem;
	}

	p.small {
		font-size: 1rem;
	}

	.tabs {
		display: flex;
		flex-flow: row wrap;
		gap: 1rem;
	}

	.tab {
		align-items: center;
		background: rgba(0, 0, 0, 0.75);
		border-radius: 8px;
		display: flex;
		flex-flow: column nowrap;
		gap: 0.25rem;
		justify-content: center;
		padding: 0.75rem 1.5rem;
		width: 150px;

		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}

	.tab * {
		color: #fff;
	}
</style>
