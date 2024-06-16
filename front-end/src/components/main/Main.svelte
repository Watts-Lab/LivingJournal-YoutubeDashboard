<script lang="ts">
	// types
	// import type Author from '../../types/Authors';
	import type ChartConfig from '../../types/ChartConfig';

	// components
	import Title from '../copy/Title.svelte';
	import Description from '../copy/Description.svelte';
	// import Authors from '../copy/Authors.svelte';
	import ScrollSection from './ScrollSection.svelte';

	// prop declaration
	export let title : string;
	export let standfirst : any[] = [{value: 'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Commodi consequatur inventore exercitationem ex perferendis provident, earum cumque maiores quam quidem labore, mollitia odit eaque laborum?'}]
	// export let authors : Author[];
	export let steps : any[]
</script>

<main>
	<Title title={ title }></Title>
	<Description standfirst={ standfirst }></Description>
	<!-- <Authors authors={ authors }></Authors> -->
	<ScrollSection { steps } />
</main>

<style lang='scss'>
	main {
		@include grid-mobile;
		@include centerH;
		align-items: center;
		max-width: $column-width;
		margin: 25px auto 0 auto;

		@media (min-width: $bp-3) {
            margin: 120px auto 0 auto;
			@include grid;
        }
	}
</style>
