<script lang="ts">
	import { onMount } from 'svelte';
	import { mobile, showSidebar } from '$lib/stores';
	import { fade } from 'svelte/transition';

	export let title = 'Souheng AI';

	// iOS standalone mode detection
	let isIOS = false;
	let isStandalone = false;
	let hasNotch = false;

	onMount(() => {
		isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;
		isStandalone =
			(window.navigator as any).standalone ||
			window.matchMedia('(display-mode: standalone)').matches;

		// Detect notch/dynamic island height for precise padding
		const safeAreaTop = parseInt(
			getComputedStyle(document.documentElement).getPropertyValue('--safe-area-inset-top') || '0'
		);
		hasNotch = safeAreaTop > 20;

		// Prevent overscroll bounce on iOS but allow internal scrolling
		if (isIOS) {
			document.body.style.overscrollBehaviorY = 'none';
			document.documentElement.style.setProperty('overflow', 'hidden');
			document.body.style.setProperty('position', 'fixed');
			document.body.style.setProperty('width', '100%');
		}
	});
</script>

<div
	class="mobile-app-shell flex flex-col h-screen overflow-hidden bg-white dark:bg-black text-gray-900 dark:text-gray-100"
	class:ios-safe-area={isIOS}
	class:has-notch={hasNotch}
>
	<!-- Header / Top Nav -->
	<header
		class="flex items-center justify-between px-4 h-16 border-b border-gray-100 dark:border-gray-800 shrink-0 bg-white/80 dark:bg-black/80 backdrop-blur-md z-20"
	>
		<button
			on:click={() => showSidebar.set(true)}
			class="p-2 -ml-2 rounded-xl active:scale-95 transition-transform hover:bg-gray-100 dark:hover:bg-gray-800"
			aria-label="Menu"
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 24 24"
				stroke-width="1.5"
				stroke="currentColor"
				class="w-6 h-6"
			>
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
				/>
			</svg>
		</button>

		<h1 class="text-base font-bold tracking-tight truncate">{title}</h1>

		<button
			class="p-2 -mr-2 rounded-xl active:scale-95 transition-transform hover:bg-gray-100 dark:hover:bg-gray-800"
			aria-label="Settings"
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 24 24"
				stroke-width="1.5"
				stroke="currentColor"
				class="w-5 h-5"
			>
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					d="M12 6.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 12.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5ZM12 18.75a.75.75 0 1 1 0-1.5.75.75 0 0 1 0 1.5Z"
				/>
			</svg>
		</button>
	</header>

	<!-- Main Content Area -->
	<main class="flex-1 overflow-y-auto overflow-x-hidden relative scroll-smooth">
		<div class="content-wrapper p-4 pb-24">
			<slot />
		</div>
	</main>

	<!-- Apple-style Tab Bar -->
	<nav
		class="tab-bar fixed bottom-0 left-0 right-0 h-20 bg-white/90 dark:bg-black/90 backdrop-blur-xl border-t border-gray-100 dark:border-gray-800 flex items-center justify-around px-6 z-30 pb-safe"
	>
		<button class="flex flex-col items-center gap-1 text-blue-600 dark:text-blue-400">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				viewBox="0 0 24 24"
				fill="currentColor"
				class="w-6 h-6"
			>
				<path
					d="M4.913 2.658c2.075-.27 4.19-.408 6.337-.417.086 0 .172 0 .25.003.078-.003.164-.003.25-.003 2.147.009 4.262.147 6.337.417 1.09.143 1.913 1.085 1.913 2.184v1.75c0 .321-.115.63-.323.872l-3.323 3.864c-.208.243-.323.551-.323.872v1.75c0 1.099-.822 2.041-1.913 2.184-2.075.27-4.19.408-6.337.417-.086 0-.172 0-.25-.003-.078.003-.164.003-.25.003-2.147-.009-4.262-.147-6.337-.417-1.09-.143-1.913-1.085-1.913-2.184V4.842c0-1.099.822-2.041 1.913-2.184Z"
				/>
				<path
					d="M12 15c-3.155 0-6.173-.487-9-1.393V18.5a3.75 3.75 0 0 0 3.75 3.75h10.5a3.75 3.75 0 0 0 3.75-3.75v-4.893c-2.827.906-5.845 1.393-9 1.393Z"
				/>
			</svg>
			<span class="text-[10px] font-medium">Chat</span>
		</button>
		<button class="flex flex-col items-center gap-1 text-gray-400 dark:text-gray-500">
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
				<path d="M11.625 16.5a1.875 1.875 0 1 0 0-3.75 1.875 1.875 0 0 0 0 3.75Z" />
				<path fill-rule="evenodd" d="M5.625 1.5H9a3.75 3.75 0 0 1 3.75 3.75v1.875c0 1.036.84 1.875 1.875 1.875H16.5a3.75 3.75 0 0 1 3.75 3.75v7.875c0 1.035-.84 1.875-1.875 1.875H5.625a1.875 1.875 0 0 1-1.875-1.875V3.375c0-1.036.84-1.875 1.875-1.875ZM12.75 12a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Zm.594 8.832a1.125 1.125 0 0 1-1.226 1.003 11.59 11.59 0 0 1-5.113-1.74 1.125 1.125 0 0 1-.34-1.488 1.125 1.125 0 0 1 1.488-.34 9.333 9.333 0 0 0 4.116 1.4 1.125 1.125 0 0 1 1.075 1.165Z" clip-rule="evenodd" />
				<path d="M14.25 5.25a1.5 1.5 0 0 1 1.5-1.5h2.625L14.25 7.875V5.25Z" />
			</svg>
			<span class="text-[10px] font-medium">History</span>
		</button>
		<button class="flex flex-col items-center gap-1 text-gray-400 dark:text-gray-500">
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
				<path fill-rule="evenodd" d="M18.685 19.097A9.723 9.723 0 0 0 21.75 12c0-5.385-4.365-9.75-9.75-9.75S2.25 6.615 2.25 12a9.723 9.723 0 0 0 3.065 7.097A9.716 9.716 0 0 0 12 21.75a9.716 9.716 0 0 0 6.685-2.653Zm-12.54-1.285A7.486 7.486 0 0 1 12 15a7.486 7.486 0 0 1 5.855 2.812A8.224 8.224 0 0 1 12 20.25a8.224 8.224 0 0 1-5.855-2.438ZM15.75 9a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Z" clip-rule="evenodd" />
			</svg>
			<span class="text-[10px] font-medium">Profile</span>
		</button>
	</nav>
</div>

<style>
	:global(html, body) {
		height: 100%;
		width: 100%;
		overflow: hidden;
		position: fixed;
		-webkit-tap-highlight-color: transparent;
	}

	.mobile-app-shell {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		user-select: none;
		-webkit-user-select: none;
	}

	.ios-safe-area header {
		padding-top: env(safe-area-inset-top);
		height: calc(4rem + env(safe-area-inset-top));
	}

	.pb-safe {
		padding-bottom: env(safe-area-inset-bottom);
	}

	/* Force hardware acceleration for smooth mobile transitions */
	main {
		transform: translateZ(0);
		-webkit-overflow-scrolling: touch;
	}

	.content-wrapper {
		min-height: 100%;
	}

	/* Active state for buttons */
	button:active {
		opacity: 0.7;
	}
</style>
