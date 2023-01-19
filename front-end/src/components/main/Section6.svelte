<script lang="ts">
    // node_modules
    import { onMount } from "svelte";
    import { csv } from "d3-fetch";
    import { autoType } from "d3-dsv";
    import { flatten } from "layercake";

    // import types
    import type Node from '../../types/Node'
    import type Link from '../../types/Link'

    // actions
    import inView from "../../actions/inView";

    // components
    import SankeyDiagram from "../graphs/SankeyDiagram.svelte";
    import HeatMap from "../graphs/HeatMap.svelte";
    
    // utils
    import enforceOrder from "../../utils/order";


    // props
    let loaded : boolean = false;
    export let once : boolean;
    export let copy : any[]
    export let refs : any[]
    export let captions : any[]

    // variable declaration
    const url_fig6 : string = 'assets/data/fig6.csv'
    let data_fig6 : any[]
    let cols : string[]

    // const sankeyTooltipFormatter = d => {
    //     if (d === 1) return 'Just as likely as average user'
    //     if (d > 1) return `More likely to consume than average user. Probability: ${d}`
    //     return `Less likely to consume than average user. Probability: ${d}`
    // }

    onMount(async () => {
        const res_fig6 = await csv(url_fig6, autoType)
        data_fig6 = res_fig6
        cols = enforceOrder(data_fig6.columns, ['fR', 'R', 'C', 'L', 'fL'])
	})

</script>

<div class="section section-6" use:inView={{ once }} on:enter={() => loaded = true }>
    {#if loaded && data_fig6}
        <HeatMap 
            data={ data_fig6 }
            url={ url_fig6 }
            spanCol={12}
            title={"YouTube consumption is reflective of user news habits"}
            caption={captions[0].value}
        />
    {:else} <div class='chart-placeholder'></div>
    {/if}
    <div class='copy'>
        {#each copy as d, i}
            <p>
                {d.value}
            </p>
        {/each}
    </div>
    <div class='references'>
        {#each refs as d, i}
            <p>
                {d.value}
            </p>
        {/each}
    </div>
</div>

<style lang='scss'>
    .section-6 {
        grid-template-columns: repeat(12, 1fr);
        column-gap: 0;
        grid-template-rows: repeat(8, auto);

        @media (min-width: $bp-3) {
            column-gap: 50px;
            grid-template-rows: auto auto auto 1fr auto;
        }
    }

    .chart-placeholder {
        height: 500px;
        background-color: lightgrey;
    }

    .section-title {
        border-bottom: 1pt solid black;
        margin: 0 0 25px 0;
        grid-row: 1 / span 1;
        grid-column: span 12;
    }

    .copy {
        grid-row: 7 / span 1;
        grid-column: span 12;

        @media (min-width: $bp-3) {
            grid-row: 5 / span 1;
            grid-column: span 7;
        }
    }

    .references {
        grid-row: 8 / span 1;
        grid-column: span 12;

        @media (min-width: $bp-3) {
            grid-row: 5 / span 1;
            grid-column: span 5;
        }
    }
</style>

