<script lang="ts">
	export let name: string | 'Anonymous'
	export let country: string | ''
	export let bio: string | undefined
	export let expandAllBios: boolean = false
	const len = 60
	let bioOpen = false
	let bioTruncated = bio?.substring(0, len)
</script>

<li class="person">
	<div class="details">
		<div class="name-title">
			<p class="name">
				{name}
			</p>
			{#if country}
				<div class="country">{country}</div>
			{/if}
		</div>
		{#if bio}
			<div class="bio">
				{#if expandAllBios}
					{bio}
				{:else}
					{bioOpen ? bio : bioTruncated}
					{#if !bioOpen && bio.length > len}
						<button on:click={() => (bioOpen = !bioOpen)}>...</button>
					{/if}
				{/if}
			</div>
		{/if}
	</div>
</li>

<style>
	.person {
		display: flex;
		gap: 1rem;
	}
	.details {
		flex-shrink: 1;
	}
	.name-title {
		border-radius: 50%;
		background-size: cover;
		background-position: center;
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 0.7rem; /* Increased from 0.5rem to 1.5rem */
	}
	@media (max-width: 600px) {
		.name-title {
			flex-direction: column;
			align-items: flex-start;
			gap: 0.25rem; /* Small gap for mobile stacked layout */
			margin-bottom: 0.5rem;
		}
	}
	.bio {
		font-style: italic;
		position: relative;
		font-size: 0.9rem;
	}
	.bio button {
		background: none;
		border: none;
		color: var(--brand);
		cursor: pointer;
		text-decoration: underline;
		font-size: 0.9rem;
		margin-left: -0.5rem;
	}
	.bio button:hover {
		color: var(--brand-dark);
		background-color: var(--bg-subtle);
		border-radius: 6px;
	}
	.bio::before {
		content: '"';
		position: absolute;
		/* make it pretty */
		color: var(--text);
		opacity: 0.1;
		font-weight: bold;
		font-size: 4rem;
		left: -1.5rem;
		top: 1.2rem;
		line-height: 0;
		margin-right: 0.5rem;
	}
	.name {
		color: var(--text);
		font-family: var(--font-heading);
		text-decoration: none;
		text-transform: capitalize;
		margin: 0;
		font-size: 1.2rem;
		font-weight: 100;
	}
	.country {
		font-weight: normal;
		font-family: var(--font-body);
		font-size: 0.9rem; /* Slightly smaller than name */
		color: var(--text-muted, #666); /* More muted color */
		opacity: 0.8; /* Subtle opacity difference */
	}
	@media (min-width: 1024px) {
		.name {
			font-size: 1.7rem;
		}
		.country {
			font-size: 1.2rem;
		}
		.bio {
			font-size: 1.2rem;
		}
	}
</style>
