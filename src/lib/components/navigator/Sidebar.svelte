<script lang="ts">
	import { Button } from '$lib/components/ui/button';
	import Icon from '$lib/components/ui/icon/icon.svelte';
	import {
		mdiAccount,
		mdiAccountMultiple,
		mdiAlarm,
		mdiBagPersonal,
		mdiBedKing,
		mdiBookshelf,
		mdiCards,
		mdiChartTimeline,
		mdiClipboardTextOutline,
		mdiCloseCircle,
		mdiCog,
		mdiDisc,
		mdiFish,
		mdiFood,
		mdiHome,
		mdiMenu,
		mdiPartyPopper,
		mdiStar,
		mdiSwordCross
	} from '@mdi/js';
	import Text from '$lib/components/typography/Text.svelte';
	import { Separator } from '$lib/components/ui/separator';
	import SidebarCategory from '$lib/components/navigator/category/SidebarCategory.svelte';
	import SidebarEntry from '$lib/components/navigator/entry/SidebarEntry.svelte';

	const paths = {
		collection: [
			{ title: 'Characters', link: '/characters', icon: mdiAccountMultiple },
			{ title: 'Weapons', link: '/weapons', icon: mdiSwordCross },
			{ title: 'Inventory', link: '/inventory', icon: mdiBagPersonal }
		],
		tracker: [
			{ title: 'To-Do', link: '/todo', icon: mdiClipboardTextOutline },
			{ title: 'Ascension', link: '/ascension', icon: mdiStar },
			{ title: 'Fishing', link: '/fishing', icon: mdiFish },
			{ title: 'Furnishing', link: '/furnishing', icon: mdiBedKing },
			{ title: 'Achievement', link: '/achievement', icon: mdiPartyPopper },
			{ title: 'Books', link: '/books', icon: mdiBookshelf },
			{ title: 'Recipes', link: '/recipes', icon: mdiFood },
			{ title: 'Spin Crystals', link: '/spin-crystals', icon: mdiDisc }
		],
		tools: [
			{ title: 'Reminder', link: '/reminder', icon: mdiAlarm },
			{ title: 'Timeline', link: '/timeline', icon: mdiChartTimeline },
			{ title: 'TCG', link: '/tcg', icon: mdiCards }
		]
	};

	let isSidebarOpen = false;

	const openSidebar = () => {
		isSidebarOpen = true;
	};

	const closeSidebar = () => {
		isSidebarOpen = false;
	};
</script>

<div
	class={`fixed flex w-full ${isSidebarOpen ? 'sm:w-72' : 'sm:w-20'} lg:w-72 ${isSidebarOpen ? 'h-full' : 'h-16'} sm:h-full flex-col z-50 p-2.5 lg:p-5 lg:pl-10 max-sm:px-5 sm:max-lg:pr-0 sm:max-lg:py-5 bg-sidebar ${isSidebarOpen ? '' : 'max-sm:rounded-b-xl'} sm:rounded-r-xl transition-all`}
>
	<div
		class={`flex ${isSidebarOpen ? 'flex-row' : 'sm:max-lg:flex-col'} items-center justify-between gap-2.5 sm:max-lg:mr-2.5`}
	>
		<div class="flex flex-row items-center">
			<div class={`rounded-full bg-red-500 w-10 h-10`} />
			<a href="/" class={`ml-2 ${isSidebarOpen ? '' : 'sm:max-lg:hidden'}`}>
				<Text type="h1">dval.in</Text>
			</a>
		</div>

		<div class="lg:hidden">
			{#if isSidebarOpen}
				<Button variant="ghost" on:click={closeSidebar}>
					<Icon path={mdiCloseCircle} size={1} color="fill-sidebarText cursor-pointer" />
				</Button>
			{/if}
			{#if !isSidebarOpen}
				<Button variant="ghost" on:click={openSidebar}>
					<Icon path={mdiMenu} size={1} color="fill-sidebarText cursor-pointer" />
				</Button>
			{/if}
		</div>
	</div>

	<div
		class={`overflow-y-auto flex flex-col flex-1 gap-1 max-sm:h-full my-2.5 pr-1 ${isSidebarOpen ? '' : 'max-sm:max-h-0 max-sm:overflow-hidden'}`}
	>
		<SidebarEntry
			title="Dashboard"
			link={'/'}
			icon={mdiHome}
			{isSidebarOpen}
			onClick={closeSidebar}
		/>
		<SidebarEntry
			title="Wish Counter"
			link={'/wish-counter'}
			icon={mdiStar}
			{isSidebarOpen}
			onClick={closeSidebar}
		/>

		<SidebarCategory
			title="Your Collection"
			paths={paths.collection}
			forceOpen={!isSidebarOpen}
			{isSidebarOpen}
			{closeSidebar}
		/>
		<SidebarCategory
			title="Trackers"
			paths={paths.tracker}
			forceOpen={!isSidebarOpen}
			{isSidebarOpen}
			{closeSidebar}
		/>
		<SidebarCategory
			title="Tools"
			paths={paths.tools}
			forceOpen={!isSidebarOpen}
			{isSidebarOpen}
			{closeSidebar}
		/>

		<div class="mt-3">
			<Separator class={`bg-white mb-3 hidden ${isSidebarOpen ? '' : 'sm:max-lg:block'}`} />
			<SidebarEntry
				title="Settings"
				link={'/settings'}
				icon={mdiCog}
				{isSidebarOpen}
				onClick={closeSidebar}
			/>
		</div>
	</div>

	<div
		class={`flex flex-row items-center justify-between sm:max-lg:mr-2.5 ${isSidebarOpen ? '' : 'max-sm:max-h-0 max-sm:overflow-hidden'}`}
	>
		<div
			class={`flex rounded-full bg-red-500 w-10 h-10 ${isSidebarOpen ? '' : 'sm:max-lg:hidden'}`}
		/>
		<div class="flex">
			<SidebarEntry
				title="Login or Register"
				link={'/login'}
				icon={mdiAccount}
				variant="default"
				{isSidebarOpen}
				onClick={closeSidebar}
			/>
		</div>
	</div>
</div>

<div
	class={`bg-black/50 transition-all absolute top-0 left-0 right-0 bottom-0 ${isSidebarOpen ? '' : 'hidden'}`}
></div>
