<script lang="ts">
	// node_modules
	import { LayerCake, Svg, Html } from 'layercake';
	import { scaleLinear, scaleOrdinal } from 'd3-scale';

	// types
	import type Channel from '../../types/Channel';

	// components
	import Force from './Force.svelte';
	import Labels from './atoms/Labels.svelte';
	import Tooltip from './tooltips/Tooltip.svelte';

	// utils
	import colorMap from '../../utils/colors';
	import labelMap from '../../utils/labels';

	// props declaration
    // export let caption: string = 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eius, tempore?';
	export let data : Channel[];
	export let currentStep : number = 0;
	// scale
	export let xKey : string = 'channel';
	export let xScale : Function = scaleLinear();
	export let xDomain : any[] = [null, null];
	export let yKey : string = 'channel';
	export let yScale : Function = scaleLinear();
	export let yDomain : any[] = [null, null];
	// z scale
	export let zKey : string = 'cluster';
	export let zScale : Function = scaleOrdinal();
	export let zDomain : any[] = Array.from(new Set(data.map(d => d.cluster)))
	export let zRange : any[] = zDomain.map(d => colorMap.get(d));
	// r scale
	export let rKey : string = 'subscribers';
	export let rRange : number[] = [5, 28];

	// variable declaration
	let evt;
	let hideTooltip : boolean|CustomEvent<any> = true;

</script>

<div id='beeswarm' class="chart beeswarm-chart">
	<LayerCake
		x={ xKey }
		{ xScale }
		{ xDomain }
		y={ yKey }
		{ yScale }
		{ yDomain }
		z={ zKey }
		{ zScale }
		{ zDomain }
		{ zRange }
		r={ rKey }
		{ rRange }
		{ data }
		padding={{ top: 50, right: 15, bottom: 15, left: 15 }}
	>

    <Svg>
      <Force
        strokeWidth={0}
        xStrength={0.1}
        yStrength={0.05}
		collideStrength={1}
		{ currentStep }
		on:mousemove={event => evt = hideTooltip = event}
		on:mouseout={() => hideTooltip = true}
      />
    </Svg>
	<Html
		pointerEvents={false}
	>
		{#if currentStep === 2}
			<Labels />
		{/if}

		{#if hideTooltip !== true && currentStep === 3}
			<Tooltip
				{evt}
				let:detail
			>
				{@const tooltipData = { ...detail.props }}
				<!-- <div class='channel-label'>{tooltipData.channel_name}</div> -->
				<div
					class='cluster-label'
					style="--color: {colorMap.get(tooltipData.cluster)}"
				>{labelMap.get(tooltipData.cluster)}</div>
				{#each ['total_videos', 'subscribers'] as key}
					{@const keyCapitalized = key.replace(/^\w/, d => d.toUpperCase()).replace('_', ' ')}
					{@const value = tooltipData[key]}
					{#if value}
						<div class="row"><span>{keyCapitalized}:</span> {value.toLocaleString()}</div>
					{/if}
				{/each}
			</Tooltip>
		{/if}
	</Html>
  </LayerCake>
</div>

<style lang='scss'>
	.chart {
		width: 100%;
		height: 600px;
		position: sticky;
		top: 10px;

		@media (min-width: $bp-3) {
			height: 500px
		}
	}

	.channel-label {
		font-weight: 700;
	}

	.cluster-label {
        color: var(--color);
        font-weight: 700;
	}
</style>