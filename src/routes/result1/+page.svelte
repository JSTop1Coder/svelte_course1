<svelte:head>
	<title>Result-1</title>
	<meta name="description" content="Result 1" />
</svelte:head>

<script>

	import { memory } from '../stores.js';
	import { onMount } from 'svelte';
	import { fly, fade } from 'svelte/transition';

	let columns = [{
		header: 'First Name',
		accessor: 'firstName'
	}, {
		header: 'Last Name',
		accessor: 'lastName'
	}, {
		header: 'Car Brand',
		accessor: 'carBrand'
	}, {
		header: 'Zip Code',
		accessor: 'zipCode'
	}, {
		header: 'Car Model',
		accessor: 'carModel'
	}, {
		header: 'First Registration',
		accessor: 'firstRegistration'
	}];
	
	
	let tableData = [];

	memory.subscribe(value => {
		tableData = value;
	});
	
	onMount(() => {
		console.log(memory);
		columns = columns.map((c) => {
			return c;
		})
	});
	
</script>

	<section>
		<div class="container">
			<div class="row text-center">
				<h2 transition:fade>Result-1</h2>
				<p transition:fade>You can see all previously entered data in here</p>
			</div>
			<hr />
			<br />
			<div class="container">
				<div class="w-100">
					<div class="pb-2">
						<span transition:fade>Total: {tableData.length}</span>
					</div>
					<table>
						<thead>
							<tr transition:fade>
								<td>No</td>
								{#each columns as column, i}
									<td>
										{column.header}
									</td>
								{/each}
							</tr>
						</thead>
				
						{#if tableData.length > 0}
							{#each tableData as row, i}
								<tr transition:fade>
									<td>{i + 1}</td>
									{#each columns as column}
										<td>
											{row[column.accessor]}
										</td>
									{/each}
								</tr>
							{/each}
						{:else }
							<tr transition:fade><td>No data</td></tr>
						{/if}
					</table>	
				</div>
			</div>
		</div>
	</section>
<style>
	.container {
		max-width: 1200px;
		margin: 0 auto;
	}

	h2 {
		margin-top: 0;
		padding: 0.75rem 0;
	}

	div {
		padding: 0 10px;
	}
	
</style>
