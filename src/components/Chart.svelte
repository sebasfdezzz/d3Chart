<script lang="ts">
	import { onMount, afterUpdate, beforeUpdate } from 'svelte';
	import * as d3 from 'd3';

	let el: HTMLElement;
	export let data: Array<number>;
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
				return (d * 5 + 35) + "px"; // 10 pixels to the right of the end
			})
			.style("top", "12px") // Adjust the top position as needed
			.style("font-weight","bold");
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
		font: 12px Arial, sans-serif;
		/*background-color: rgba(139, 0, 0, 0.7); /* Darker red with some transparency */
		background: #ff5353!important;
		text-align: center; /* Center text for a modern look */
		padding: 10px; /* More padding for a modern and spacious feel */
		margin: 5px; /* Slightly more margin for separation */
		color: white;
		border-radius: 10px; /* Rounded corners for a sophisticated look */
		box-shadow: 1px 4px 3px #00000017, 0 0 0 3px #fff3;
		transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
		position: relative;
		/*border: 2px solid black; /* Black border */
	}

	.chart :global(div.bar .percentage) {
		font-size: 14px; /* Slightly larger font for emphasis */
		color: black;
	}

	.chart :global(div.bar:hover) {
		background-color: rgba(139, 0, 0, 0.9); /* Darker red on hover for an interactive effect */
		transform: scale(1.05); /* Slight scaling on hover for depth */
		box-shadow: 0 0 20px rgba(139, 0, 0, 0.9); /* Enhanced glowing shadow on hover */
	}
</style>



<div bind:this={el} class="chart"></div>
