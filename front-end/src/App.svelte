<script lang="ts">
	// types
	import type Data from './types/Data';
	import type Author from './types/Authors';

	// sections
	import Header from './components/header/Header.svelte';
	import Footer from './components/footer/Footer.svelte';
	import Main from './components/main/Main.svelte';
	import Section1 from './components/main/Section1.svelte';
	import Section2 from './components/main/Section2.svelte';
	import Section3 from './components/main/Section3.svelte';
	import Section4 from './components/main/Section4.svelte';
	import Section5 from './components/main/Section5.svelte';
	import Section6 from './components/main/Section6.svelte';
	import Section7 from './components/main/Section7.svelte';
	import Section8 from './components/main/Section8.svelte';
	import Supplementary from './components/main/Supplementary.svelte';

	// export let title : string = 'Your title goes here';
	// export let standfirst : any[]
	export let data : Data
	export let authors : Author[];
</script>

<Header />
<Main title={ data.title } { authors } standfirst={ data.standfirst } steps={ data.scroller } />
<Section1 once={ true } copy={data['section-one'].copy} refs={data['section-one'].references} captions={data['section-one'].captions} markers={data['markers']}/>
<Section2 once={ true } copy={data['section-two'].copy} refs={data['section-two'].references} captions={data['section-two'].captions} markers={data['markers']}/>
<Section3 once={ true } copy={data['section-three'].copy} refs={data['section-three'].references} captions={data['section-three'].captions} />
<Section4 once={ true } copy={data['section-four'].copy} refs={data['section-four'].references} captions={data['section-four'].captions} />
<Section5 once={ true } copy={data['section-five'].copy} refs={data['section-five'].references} captions={data['section-five'].captions} />
<Section6 once={ true } copy={data['section-six'].copy} refs={data['section-six'].references} captions={data['section-six'].captions} />
<Section7 once={ true } copy={data['section-seven'].copy} refs={data['section-seven'].references} captions={data['section-seven'].captions} />
<Section8 once={ true } copy={data['section-eight'].copy} refs={data['section-eight'].references} captions={data['section-eight'].captions} />
<Supplementary once={ true } copy={data['supplementary'].copy} refs={data['supplementary'].references} captions={data['supplementary'].captions} />
<Footer />

<style lang='scss' global>
	main, .section {
		padding: 0 1em;
	}
	@media (min-width: $column-width) {
		main, .section {
			padding: 0
		}
	}
	.section {
		max-width: $column-width;
		margin: 3em auto;
		display: grid;
	}

	.section:last-of-type {
		margin-bottom: 5em;
	}

	.chart {
		height: 500px;
	}

	.chart-medium {
		height: 400px;
	}

	.caption {
		@include fs-sm;
		font-weight: 300;
	}

	.copy {
		margin: 0;

		@media (min-width: $bp-3) {
			margin: 35px 0 0 0;
		}

		p {
			margin: 10px 0;
			@include fs-root;

			@media (min-width: $bp-2) {
				@include fs-md;
			}
		}
	}

	.references {
		margin: 0;

		@media (min-width: $bp-3) {
			margin: 35px 0;
		}

		p {
			margin: 10px 0;
			line-height: 1.6;
			@include fs-sm;
		}
	}

	.link.inactive {
			stroke-opacity: 0.15 !important;
	}
	.link.active {
			stroke-opacity: 0.5 !important;
	}

	.heat-map-cell.active {
		border: 1pt solid $black !important;
	}

	.group-rect.inactive, 
	.range-circle.inactive {
        opacity: 0.5 !important;
    }
	
	.group-rect.active,
	.range-circle.active {
        opacity: 1 !important;
    }

	.active-node {
		stroke: black;
		stroke-width: 2pt; 
	}
</style>