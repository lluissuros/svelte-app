<svelte:head>
	<link rel="preconnect" href="https://fonts.gstatic.com">
	<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap" rel="stylesheet">
</svelte:head>


<script>
	let initialSalary = 60000
	let years = 5;
	let percentage = 15;
	let salariesPerYear = []
	let averagedSalary
	
 	$: salariesPerYear = computeSalaries(initialSalary, years, percentage)
	$: averagedSalary = computeAveraged(salariesPerYear)
	
	function computeSalaries(initialValue, years, percentage) 	{
 		const dummyInit = new Array(years-1).fill(0)
		
		return dummyInit.reduce((acc, val, i)=> {
			const newSalary = acc[i] * (1 + percentage/100)
			return acc.concat(Math.ceil(newSalary))
		}, [initialValue])
	}
	
	function computeAveraged(numbers) {
		const aggregated = numbers.reduce((acc, val)=>{
			return acc + val
		}, 0) 
		return aggregated / numbers.length
	}
</script>

<style>
	:global(body) {
		background-color: white;
		color:#222222;
		font-family: 'Roboto', 'Noto', sans-serif;
		font-size: 16px;
		line-height: 24px;
	}

	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
		max-width: 250px;
	}

	h1 {
		text-transform: uppercase;
		line-height: 34px;
		font-size: 2em;
		font-weight: 100;
	}

	h3 {
		margin-bottom: 4px;
	}

	.slidersContainer{
		background-color:#f2fbff;
		border-radius: 4px;
		padding: 16px 0;
	}

	.title {
		color:#2196F3;
	}

	.left {
		text-align: left;
		font-weight: 100;
		margin-left: 16px
	}


</style>


<main>
<h1 class="title">Salary calculator</h1>



<div class="slidersContainer">
	<div class="title left">👇Percentage</div>
	<label>
		<input type=number bind:value={percentage} min=0 max=20>
		<input type=range bind:value={percentage} min=0 max=20>
	</label>
<br/>

	<div class="left title">👇Years</div>
	<label>
		<input type=number bind:value={years} min=1 max=10>
		<input type=range bind:value={years} min=1 max=10>
	</label>
</div>




<div>
<h3 class="title">Averaged salary</h3>
{averagedSalary}	
</div>

<br/>

<h3 class="title">Salary per year</h3>
{#each salariesPerYear as salary, i}
 <div>
	 year {i+1}: {salary}
</div>
{/each}


</main>
