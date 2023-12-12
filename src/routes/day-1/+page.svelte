<script lang="ts">
	import elvesData from './data.json';
	import PersonCard from './PersonCard.svelte';

	let name: string;

	let personDetails = elvesData;

	const findPerson = () => {
		if (name) {
			let searchResults = elvesData.filter((person) => {
				return person.name.toLocaleLowerCase().includes(name.toLocaleLowerCase());
			});
			if (searchResults.length > 0) {
				personDetails = searchResults;
			} else {
				personDetails = [];
			}
		} else {
			personDetails = elvesData;
		}
	};
</script>

<main class="flex flex-col justify-center items-center p-5 gap-5">
	<h1 class="text-4xl text-center font-medium text-rose-600">Day 1: Naughty 😈 or Nice 😇</h1>

	<input
		type="search"
		name="name"
		id="name"
		bind:value={name}
		on:input={findPerson}
		placeholder="Enter name to search"
		class="border-2 border-rose-300 p-2 text-xl text-center rounded-md focus:drop-shadow-2xl focus:border-rose-600 outline-none accent-inherit"
	/>

	<div class="flex gap-5">
		<button
			on:click={() => {
				personDetails = elvesData;
			}}>all</button
		>
		<button
			on:click={() => {
				personDetails = elvesData.filter((person) => person.tally > 0);
			}}>nice</button
		>
		<button
			on:click={() => {
				personDetails = elvesData.filter((person) => person.tally <= 0);
			}}>naughty</button
		>
	</div>

	<section class="grid grid-cols-2 sm:grid-cols-4 gap-5">
		{#if personDetails.length > 0}
			{#each personDetails as { name, tally }}
				<PersonCard {name} score={tally} />
			{/each}
		{:else}
			<p>No person with '{name}' name found!</p>
		{/if}
	</section>
</main>

<style lang="postcss">
	button {
		@apply rounded-md bg-green-500 p-3 uppercase text-white hover:bg-green-900;
	}
</style>
