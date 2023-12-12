<script lang="ts">
	export let name: string, score: number;
</script>

<div
	class="relative flex flex-col justify-center items-center px-5 py-7 rounded-md bg-gray-100 shadow-lg hover:shadow-2xl text-gray-600 group {score >
	0
		? 'hover:text-green-500'
		: 'hover:text-rose-600'}"
>
	{#if score > 0}
		<img src="/images/innocent-emoji.webp" alt="nice" class="emoji" />
	{:else}
		<img src="/images/devil-emoji.webp" alt="naughty" class="emoji" />
	{/if}
	<p class="text-3xl z-10">{name}</p>
	<p
		class="bg-white h-10 w-10 flex items-center justify-center rounded-full z-10 mt-2 invisible group-hover:visible"
	>
		{score}
	</p>
</div>

<style lang="postcss">
	/* .emoji {
		@apply absolute inset-0 -z-10 opacity-25;
	} */
	.emoji {
		@apply absolute left-1/2 top-1/2 h-20 w-20 -translate-x-1/2 -translate-y-1/2 opacity-5 group-hover:opacity-[15%];
	}
</style>
