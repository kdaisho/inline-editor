<script lang="ts">
	let editable = false;

	const toggleEditable = () => {
		editable = !editable;
	};

	let data: Record<string, null | HTMLElement> = {
		title: null,
		p1: null,
		p2: null,
		tag1: null,
		tag2: null,
	};

	$: {
		if (!editable) {
			Object.entries(data).forEach(([_, value]) => {
				console.log(value?.innerText);
			});
		}
	}

	let tags = [
		{
			lead: "Always something",
			text: "5 years of noise",
		},
	];

	const addTag = () => {
		tags = [...tags, { lead: "New tag", text: "New subtitle" }];
	};
</script>

<div class="control">
	<button class="is-btn" on:click={toggleEditable}>
		{#if editable}
			Save
		{:else}
			Edit
		{/if}
	</button>
</div>

<section class:is-editing={editable}>
	<h1>Product Name</h1>

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

	<div class="group" class:is-editable={editable}>
		<div class="tags" contenteditable={editable}>
			{#each tags as tag}
				<span class="tag">
					<h3>{tag.lead}</h3>
					<p class="small">{tag.text}</p>
				</span>
			{/each}
		</div>

		{#if editable}
			<button class="is-add" on:click={addTag}>+</button>
		{/if}
	</div>
</section>

<style>
	/* .edit :is(h1, h3, p) {
    } */

	/* .is-editable {
		border-radius: var(--radius);
		display: flex;
		flex-flow: column nowrap;
		gap: 1rem;
		padding: 0.25rem;
	} */

	.control {
		position: fixed;
		top: 20px;
		right: 200px;
		z-index: 1;
	}

	.group {
		display: inline;
		width: auto;
	}

	button.is-btn {
		border-radius: var(--radius);
		color: #fff;
		padding: 0.75rem 1.5rem;
	}

	button.is-add {
		align-items: center;
		background: var(--theme);
		border-radius: 35px;
		color: #fff;
		display: flex;
		font-size: 1rem;
		justify-content: center;
		height: 30px;
		width: 30px;
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

	[contenteditable] {
		outline: none;
	}

	.is-editing [contenteditable] {
		outline: 1px solid var(--theme);
		outline-offset: 0.25rem;
		border-radius: var(--radius-small);
	}

	.is-editing [contenteditable]:focus {
		outline: 2px solid var(--theme);
	}

	.tags {
		display: inline-flex;
		flex-flow: row wrap;
		gap: 1rem;
	}

	.tag {
		align-items: center;
		background: rgba(0, 0, 0, 0.75);
		border-radius: var(--radius);
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

	.tag * {
		color: #fff;
	}
</style>
