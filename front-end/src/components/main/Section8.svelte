<script lang="ts">
    // node_modules
    import { onMount } from "svelte";
    import { csv } from "d3-fetch";
    import { autoType } from "d3-dsv";
    
    // actions
    import inView from "../../actions/inView";

    // components
    import StackedBars from "../graphs/StackedBars.svelte";

    // utils
    import { youTubeMap as labelMap } from "../../utils/labels";
    import { youTubeMap as colorMap } from "../../utils/colors";
    import { formatPct } from '../../utils/format-numbers';

    // props
    let loaded : boolean = false;
    export let once : boolean;
    export let copy : any[]
    export let refs : any[]
    export let captions : any[]

    // variable declaration
    let url_table2 : string = 'assets/data/table2.csv'
    let data_table2 : any[]
    let xKey : number[] = [0,1]
    let yKey : string = 'cluster'
    let zKey : string = 'key'

    onMount(async () => {
        const res = await csv(url_table2, autoType)
        data_table2 = res
	})
</script>

<div class="section section-8" use:inView={{ once }} on:enter={() => loaded = true }>
    {#if loaded && data_table2}
        <StackedBars 
            data={ data_table2 } 
            { yKey } 
            { xKey } 
            { zKey } 
            formatter={formatPct(2)}
            keyColorMap={ colorMap }
            keyLabelMap={ labelMap }
            url={ url_table2 }
            spanCol={12}
            row={3}
            customClass={'chart-medium'}
            title={'How users arrive at political content'}
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
    .section-8 {
        grid-template-columns: repeat(12, 1fr);
        column-gap: 0;
        grid-template-rows: auto auto auto 1fr auto auto;

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
        grid-row: 5 / span 1;
        grid-column: span 12;

        @media (min-width: $bp-3) {
            grid-column: span 7;
        }
    }

    .references {
        grid-row: 6 / span 1;
        grid-column: span 12;

        @media (min-width: $bp-3) {
            grid-row: 5 / span 1;
            grid-column: span 5;
        }
    }
</style>