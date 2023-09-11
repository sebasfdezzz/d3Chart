<script>
	import { onMount, afterUpdate, beforeUpdate } from 'svelte';
	import * as d3 from 'd3';

	let el;
	export let data;

	function updateChart() {
		// Remove existing bars and percentages
		d3.select(el).selectAll("div").remove();

		// Create new bars
		const bars = d3.select(el)
			.selectAll("div")
			.data(data)
			.enter()
			.append("div")
			.style("width", function(d) {
				return d * 5 + "px";
			})
			.style("height", "25px")
			.attr("class", "bar");

		// Position the text to the right of the end of each div
		bars.append("span")
			.attr("class", "percentage")
			.text(function(d) {
				return d + "%";
			})
			.style("position", "absolute")
			.style("left", function(d) {
				return (d * 5 + 10) + "px"; // 10 pixels to the right of the end
			})
			.style("top", "3px"); // Adjust the top position as needed
	}

	onMount(() => {
		updateChart();
	});

	beforeUpdate(() => {
		// This is called before the data updates, remove the old chart
		d3.select(el).selectAll("div").remove();

		// Call updateChart to display the chart initially and when data changes
		updateChart();
	});

	afterUpdate(() => {
		// This is called after the data updates, create the updated chart
		updateChart();
	});
</script>

<style>
	.chart :global(div.bar) {
		font: 10px sans-serif;
		background-color: steelblue;
		text-align: right;
		padding: 3px;
		margin: 1px;
		color: white;
		position: relative;
	}

	.chart :global(div.bar .percentage) {
		font: 10px sans-serif;
		color: black;
	}
</style>

<div bind:this={el} class="chart"></div>
