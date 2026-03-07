<script lang="ts">
	import { mobile, showSidebar } from '$lib/stores';
	import { getContext } from 'svelte';
	const i18n = getContext('i18n');

	export let title = 'Souheng AI';
</script>

<nav class="flex items-center justify-between px-4 pt-[env(safe-area-inset-top)] pb-2 bg-white/80 dark:bg-gray-900/80 backdrop-blur-md border-b dark:border-gray-800 h-[calc(3.5rem+env(safe-area-inset-top))] sticky top-0 z-50 md:hidden shadow-sm">
	<button
		class="p-2 hover:bg-gray-100 dark:hover:bg-gray-800 rounded-lg transition"
		on:click={() => showSidebar.set(true)}
		aria-label="Open Sidebar"
	>
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-6 h-6">
			<line x1="3" y1="12" x2="21" y2="12"></line>
			<line x1="3" y1="6" x2="21" y2="6"></line>
			<line x1="3" y1="18" x2="21" y2="18"></line>
		</svg>
	</button>

	<span class="font-bold text-gray-900 dark:text-white truncate mx-4">
		{title}
	</span>

	<div class="w-10">
		<!-- Space for right-side action or just for centering -->
	</div>
</nav>
