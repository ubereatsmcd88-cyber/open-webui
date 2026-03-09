<script lang="ts">
	import { mobile, showSidebar } from '$lib/stores';
	import { getContext } from 'svelte';
	const i18n = getContext('i18n');

	export let title = 'Souheng AI';
</script>

<nav
	class="flex items-center justify-between px-4 pt-[env(safe-area-inset-top)] bg-white/80 dark:bg-black/80 backdrop-blur-xl border-b border-gray-100 dark:border-gray-900 h-[calc(4rem+env(safe-area-inset-top))] sticky top-0 z-50 md:hidden"
>
	<button
		class="p-2 -ml-1 rounded-xl active:scale-95 transition-transform hover:bg-gray-100 dark:hover:bg-gray-900"
		on:click={() => showSidebar.set(true)}
		aria-label="Open Sidebar"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="w-6 h-6"
		>
			<line x1="3" y1="12" x2="21" y2="12"></line>
			<line x1="3" y1="6" x2="21" y2="6"></line>
			<line x1="3" y1="18" x2="21" y2="18"></line>
		</svg>
	</button>

	<span class="font-bold text-base tracking-tight text-gray-900 dark:text-white truncate">
		{title}
	</span>

	<button
		class="p-2 -mr-1 rounded-xl active:scale-95 transition-transform hover:bg-gray-100 dark:hover:bg-gray-900"
		aria-label="New Chat"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="w-5 h-5"
		>
			<path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
			<path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
		</svg>
	</button>
</nav>
