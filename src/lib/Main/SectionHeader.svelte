<script lang="ts">
	import { editMode } from '$lib/Stores';
	import DragIndicator from '$lib/Main/DragIndicator.svelte';
	import DeleteButton from '$lib/Main/DeleteButton.svelte';
	import SectionTitle from '$lib/Main/SectionTitle.svelte';

	export let view: any;
	export let section: any;
</script>

<header>
	<h1 style:cursor={$editMode ? 'text' : 'initial'}>
		{#if $editMode}
			<SectionTitle bind:value={section.name} />
		{:else if section?.name === ''}
			{@html '&nbsp;'}
		{:else}
			{section?.name}
		{/if}
	</h1>

	{#if $editMode}
		<div class="right">
			<DragIndicator />

			<!-- can't be asynchronously loaded, it'll flash on dnd -->
			<DeleteButton {view} {section} />
		</div>
	{/if}
</header>

<style>
	header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		color: var(--theme-colors-title);
	}

	header h1 {
		padding: 0;
		font-size: 1.8rem;
		font-weight: 600;
		margin-block-start: 0;
		margin-block-end: 0.4rem;
	}

	.right {
		display: flex;
	}
</style>
