<script lang="ts">
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';
	import { answers, type Answer } from '../../store';
	let answersValue: Answer[] = [];

	answers.subscribe((value) => {
		answersValue = value;
	});

	const numberOfQuestions = answersValue.length;
	const numberOfCorrectAnswers = answersValue.reduce((sum, answer) => {
		if (answer.isCorrect) {
			return sum + 1;
		}
		return sum;
	}, 0);

	const handleBack = () => {
		answers.set([]);
		goto('/');
	};

	onMount(() => {
		if (!answersValue.length) goto('/');
	});
</script>

<div class="text-center">
	<h1 class="text-7xl font-bold">
		{((numberOfCorrectAnswers / numberOfQuestions) * 100).toFixed(0)}%
	</h1>
	<p class="text-xl text-gray-500">{numberOfCorrectAnswers}/{numberOfQuestions}</p>
	<button
		class="mt-3 w-full bg-blue-500 py-2 px-5 rounded-lg text-lg text-white"
		on:click={handleBack}>Go Back</button
	>
</div>
