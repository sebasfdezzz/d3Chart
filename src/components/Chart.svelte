<script lang="ts">
	import { onMount, afterUpdate, beforeUpdate } from 'svelte';
	import * as d3 from 'd3';

	let el: HTMLElement;
	export let data: Array<{ label: string, value: number }>;

	function updateChart() {
		d3.select(el).selectAll("div").remove();

		const bars = d3.select(el)
			.selectAll("div")
			.data(data)
			.enter()
			.append("div")
			.attr("class", "bar")
			.style("margin", "15px 0 15px 0");

		const labelValueContainer = bars.append("div")
			.attr("class", "label-value-container");

		labelValueContainer.append("span")
			.attr("class", "label")
			.text(d => d.label)
			.style("position", "absolute")
			.style("font-size", "14px")
			.style("color","rgb(220, 220, 220)")
			.style("left", function(d) {
				const labelWidth = this.getBoundingClientRect().width;
				return (-labelWidth - 10) + "px";
			})
			.style("top", "10px");

		labelValueContainer.append("span")
			.attr("class", "value")
			.text(d => d.value + "%")
			.style("position", "absolute")
			.style("font-size", "14px")
			.style("left", function(d) {
				return (d.value * 8 + 35) + "px";
			})
			.style("top", "10px")
			.style("font-weight","bold");

		bars.style("width", function (d) {
			return d.value * 8 + "px";
		})
		.style("height", "10px")
		.attr("class", "bar");
	}
	onMount(() => {
		updateChart();
	});

	beforeUpdate(() => {
		d3.select(el).selectAll("div").remove();
		updateChart();
	});

	afterUpdate(() => {
		updateChart();
	});
</script>

<style>
	.chart :global(div.bar) {
		font: 12px Arial, sans-serif;
		background: #ff5353!important;
		text-align: center;
		padding: 10px;
		margin: 5px;
		color: white;
		border-radius: 10px;
		box-shadow: 1px 4px 3px #00000017, 0 0 0 3px #fff3;
		transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
		position: relative;
		margin-left:100px ;
	}

	.chart :global(div.label-value-container) {
		display: flex;
		justify-content: space-between;
	}

	.chart :global(div.label),
	.chart :global(div.value){
		font-size: 20px;
		color: black;
	}

	.chart :global(div.bar:hover) {
		background-color: rgba(139, 0, 0, 0.9);
		transform: scale(1.05);
		box-shadow: 0 0 20px rgba(139, 0, 0, 0.9);
	}
</style>

<div bind:this={el} class="chart" style="margin-left: 300px; margin-top: 50px;"></div>

