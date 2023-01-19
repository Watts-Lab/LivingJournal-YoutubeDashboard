<script lang="ts">
  // node_modules
  import { LayerCake, Html } from 'layercake';
  import { scaleDiverging } from 'd3-scale';

  // import components
  import Caption from './atoms/Caption.svelte';
  import HeatMapGrid from './atoms/HeatMapGrid.svelte';
  import ColorLegend from './atoms/ColorLegend.svelte';
  import Tooltip from './tooltips/Tooltip.svelte';

  // import maps
  import labelMap from '../../utils/labels';
  import colorMap from '../../utils/colors';

  // props declaration
  export let data : any[];
  export let url : string;
  export let caption: string = 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eius, tempore?';
  export let includeCaption : boolean = true;
  export let spanCol : number = 12;
  export let title : string;

  // variable declaration
  let evt;
  let hideTooltip : boolean|CustomEvent<any> = true;
  
  const scaleColor = scaleDiverging()
    .domain([-1, 1, 3])
    .range(['#317873', '#eee', '#E08A00'])
</script>

{#if title}<div class="chart-title {spanCol === 12 ? 'title-split-cols' : 'title-single-cols'}"><h3>{title}</h3> <ColorLegend scale={ scaleColor }/></div>{/if}
<div 
    class={`chart-wrapper ${spanCol === 12 ? 'split-cols' : 'single-cols'}`} 
    style={`--spanCol: ${spanCol}`}
>
  <div class="chart heat-map">
    <LayerCake
        { data }
        padding={{
            top: 10,
            bottom: 0,
            left: 50,
            right: 0,
        }}
        position={'relative'}
        custom={{ scaleColor }}
    >
        <Html>
          <div class='axis axis-y'>YouTube Community</div>
          <div class='axis axis-x'>Web News Category</div>
          <HeatMapGrid 
            on:mousemove={event => evt = hideTooltip = event}
            on:mouseout={() => hideTooltip = true}
          />
          {#if hideTooltip !== true}
            <Tooltip
                {evt}
                offset={-10}
                let:detail
            > 
                {@const tooltipData = { ...detail.props }}
                <div>
                    <span 
                        class='cluster-label'
                        style="--color: {colorMap.get(tooltipData.to)}"
                    >
                        {labelMap.get(tooltipData.to)}
                    </span> ➞
                    <span
                        class='cluster-label'
                        style="--color: {colorMap.get(tooltipData.from)}"
                    >
                        {labelMap.get(tooltipData.from)}
                    </span>
                </div>
                {#each ['value'] as key}
                    {@const value = tooltipData[key]}
                    <div class="row">Risk ratio: {value}</div>
                {/each}
            </Tooltip>
          {/if}
        </Html>
    </LayerCake>
  </div>
  {#if includeCaption}
      <Caption { caption } { url } type={spanCol === 12 ? 'split-cols' : 'single-cols'}/>
  {/if}
</div>

<style lang='scss'>
  .chart-title {
    display: inline-flex;
    gap: 10px;
    align-items: center;
    flex-wrap: wrap;

    h3 {
        width: 100%;

        @media (min-width: $bp-3) {
            width: auto;
        }
    }
  }
  
  .title-split-cols {
      grid-column: 1 / span 12;
      grid-row: 1 / span 1;
  }

  .title-single-cols {
      grid-column: 1 / span 12;
      grid-row: 3 / span 1;
      margin-top: 25px;

      @media (min-width: $bp-3) {
          grid-column: 7 / span 6;
          grid-row: 1 / span 1;
          margin-top: 0;
      }
  }

  .chart-wrapper {
      display: grid;
      grid-template-columns: 1fr;
      row-gap: 10px;
      column-gap: 10px;
      grid-row: 2 / span 1;
      grid-column: span 12;

      @media (min-width: $bp-3) {
          grid-column: span var(--spanCol);
          grid-row: 2 / span 1;
      }
  }

  .cluster-label {
        color: var(--color);
        font-weight: 700;
    }

  .split-cols {
      grid-template-columns: 1fr;

      @media (min-width: $bp-3) {
          grid-template-columns: 10fr 2fr;
      }
  }

  .single-cols {
      grid-template-columns: 1fr;
      grid-template-rows: auto 1fr;
      grid-row: 4 / span 1;

      @media (min-width: $bp-3) {
          grid-row: 2 / span 1; 
      }
  }

  .axis {
    position: absolute;
    color: $dark-grey;
    font-weight: 300 !important;
    text-transform: uppercase;
    @include fs-sm;
  }

  .axis-x {
    top: 0;
    left: 50%;
    transform: translate(calc(-50% + 32px),0);
  }

  .axis-y {
    top: calc(50% + 10px);
    left: 0;
    transform: translate(-65%, 0) rotate(-90deg);
  }
</style>