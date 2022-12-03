<script lang="ts">
	import {
		Badge,
		Button,
		ButtonGroup,
		Card,
		Checkbox,
		Input,
		Label,
		Listgroup,
		ListgroupItem
	} from 'flowbite-svelte';

	let list: { id: Symbol; name: string }[] = [];
	let selectedItems: { id: Symbol; name: string }[] = [];

	let inputValue = '';

	function addToSelected(item: { id: Symbol; name: string }) {
		if (!selectedItems.find((i) => i.id === item.id)) {
			selectedItems = [...selectedItems, item];
		} else {
			selectedItems = selectedItems.filter((i) => i.id !== item.id);
		}
	}

	function addItem() {
		if (inputValue !== '') {
			list = [...list, { id: Symbol(), name: inputValue }];
		}
		inputValue = '';
	}

	function removeSelectedItems() {
		list = list.filter((n) => {
			return !selectedItems.includes(n);
		});
		selectedItems = [];
	}

</script>

<Card class="w-96 m-auto mt-10">
	<Badge color="green" baseClass="block self-end">New!</Badge>
	<h5 class="mb-5 text-2xl font-semi-bold tracking-tight text-gray-900 self-center">
		Simple Todo list
	</h5>
	<form on:submit|preventDefault>
		<Label id="todo-input">Enter an item</Label>
		<ButtonGroup class="w-full mb-14">
			<Input id="todo-input" bind:value={inputValue} />
			<Button type='submit' color="blue" on:click={addItem}>Add</Button>
		</ButtonGroup>
	</form>
	{#if list.length > 0}
		<Listgroup class="mb-5">
			{#each list as item (item.id)}
				<div>
					<ListgroupItem>
						<Checkbox on:click={() => addToSelected(item)}>
							<span class="ml-2" class:checked={selectedItems.find((i) => i.id === item.id)}
								>{item.name}</span
							>
						</Checkbox>
					</ListgroupItem>
				</div>
			{/each}
		</Listgroup>
	{/if}
	<div class="grid grid-cols-2 gap-4 place-content-around">
		<div class="contents">
			<Button disabled={!(selectedItems.length > 0)} color="red" on:click={removeSelectedItems}>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="20"
					height="20"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
					class="feather feather-trash mr-2"
					><polyline points="3 6 5 6 21 6" /><path
						d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"
					/></svg
				> Remove checked
			</Button>
		</div>
		<div class="contents">
			<Button disabled={true} color="dark">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="20"
					height="20"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
					class="feather feather-edit mr-4"
					><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7" /><path
						d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"
					/></svg
				>Edit item
			</Button>
		</div>
	</div>
</Card>

<style>
	.checked {
		text-decoration: line-through;
	}
</style>
