<script>
	import quizzes from '../data.json';
	import Card from '../components/Card.svelte';
</script>

<h1>This is a test</h1>
{#each quizzes as quiz (quiz.id)}
	<Card {quiz} />
{/each}

<style lang="postcss">
</style>
