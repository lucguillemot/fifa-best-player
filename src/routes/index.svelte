<script>
	import Dotplot from '../components/Dotplot.svelte';
</script>

<div>
	<h1>Who’s the Best Player in FIFA?</h1>
	<p>
		It depends on what you look at. You may pass on sliding tackles to reach the top, but you can’t
		do without good reactions skill.
	</p>
	<Dotplot />
</div>

<style>
	h1 {
		font-size: 4.5rem;
		text-align: center;
		max-width: 600px;
		margin: 0 auto;
	}
	p {
		font-size: 1rem;
		text-align: center;
		margin: 0 auto;
		max-width: 600px;
	}
</style>
