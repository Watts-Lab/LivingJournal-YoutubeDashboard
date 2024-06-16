<script lang="ts">
  import type Author from '../../types/Authors';

  export let authors : Author[];
</script>

<div class="section container">
  <div class='line'></div>
  <div class='title'>The Team</div>
  <div class='authors'>
    {#each authors as author}
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <div 
        class='author-container'
        >
        <div class='author-photo' style="--photo-url: url('https://watts-lab.github.io/LivingJournal-YoutubeDashboard/assets/images/{author.photo}')"></div>
        <a class='author-bio' href={author.url}>
          <p class='author-name'>{author.name}</p>
          <p class='author-desc'>{author.desc}</p>
        </a>
      </div>
    {/each}
  </div>
</div>

<style lang="scss">
  .container  {
    display: grid;
    grid-template-columns: repeat(8, 1fr);
    grid-template-rows: auto auto 1fr; 
    grid-column-gap: 10px;
    grid-row-gap: 10px;
    margin-bottom: 3em;

    @media (min-width: $bp-3) {
      grid-template-columns: repeat(12, 1fr);
      grid-template-rows: auto auto 1fr; 
    }
  }

	.authors {
		grid-column: 1 / span last-line;
		grid-row: 3 / span 1;
		display: flex;
		flex-wrap: wrap;
		column-gap: 10px;
		row-gap: 8px;

		@media (min-width: $bp-3) {
			grid-row: 3 / span 1;
			grid-column: 1 / span 12;
		}

		.author-container {
			display: inline-flex;
			margin: 0;
			position: relative;
			width: 100%;
			column-gap: 5px;

			@media (min-width: $bp-1) {
				width: 32%;
			}

			.author-photo {
				width: 45px;
				height: 45px;
				background-size: cover;
				background-position: center;
				background-image: var(--photo-url);
				border-radius: 50%;
				flex-grow: 0;
				flex-shrink: 0;
			}

			.author-bio {
				display: grid;
				grid-template-columns: 1fr;
				grid-template-rows: 0.3fr 0.7fr;
				color: $black;
			}

			.author-bio:hover {
				opacity: 0.9;
			}

			.author-bio:visited {
				color: $black;
			}

			.author-name {
				font-weight: 500;
				display: inline;
				pointer-events: none;
				@include fs-sm;

				@media (min-width: $bp-3) {
					@include fs-root;
				}
			}
			.author-desc {
				font-weight: 300;
				display: inline;
				pointer-events: none;
				@include fs-xs;

				@media (min-width: $bp-3) {
					@include fs-sm;
				}
			}
    }
  }

	.line {
		grid-column: 1 / span 8;
		width: 25%;
		height: 1px;
		background-color: $black;
		margin: 10px 0;

		@media (min-width: $bp-3) {
			grid-row: 1 / span 1;
			grid-column: 1 / span 8;

		}
	}

	.title {
		grid-column: 1 / span 8;
		@include fs-root;
		font-weight: 700;
		margin-bottom: 10px;

		@media (min-width: $bp-3) {
			grid-row: 2 / span 1;
			grid-column: 1 / span 8;
    }
  }
</style>
