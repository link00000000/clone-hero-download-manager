<template>
  <div id="app">
    <!-- More Options Dropdown Content -->
    <ul id="more-options" class="dropdown-content">
        <li><a href="#!">Preferences</a></li>
        <li><a href="#!">Add Source</a></li>
    </ul>

    <!-- Nav Bar -->
    <div class="navbar-fixed">
		<nav class="nav-extended">
			<div class="nav-content">
				<ul class="tabs tabs-transparent">
					<li class="tab"><a href="#landingPage">Home</a></li>
					<li class="tab"><a href="#managerPage">Manage Songs</a></li>
					<li class="tab"><a href="#searchPage">Find Songs</a></li>
					<li class="tab"><a href="#downloadPage">Downloads</a></li>
					<li class="right"><a class="dropdown-trigger" href="#!" data-target="more-options"><i class="material-icons right">more_vert</i></a></li>
				</ul>
			</div>
		</nav>
	</div>

    <!-- Page Content -->
    <div class="container">
        <div class="row">
            <div id="landingPage" class="col s12"><landing-page></landing-page></div>
            <div id="managerPage" class="col s12"><manager-page></manager-page></div>
            <div id="searchPage" class="col s12"><search-page></search-page></div>
            <div id="downloadPage" class="col s12"><download-page></download-page></div>
        </div>
      </div>
  </div>
</template>

<script>
	import landingPage from '@/layouts/LandingPage'
	import managerPage from '@/layouts/ManagerPage'
	import searchPage from '@/layouts/SearchPage'
	import downloadPage from '@/layouts/DownloadPage'

	export default {
		name: 'clone-hero-download-manager',
		components: {
			landingPage,
			managerPage,
			searchPage,
			downloadPage
		},
		mounted() {
			// Initialize tabbed menu
			let tabbedMenuInstance = M.Tabs.init(this.$el.querySelector('.tabs'));

			// Initialize more options dropdown
			const moreOptionsDropdownOptions = {
				constrainWidth: false,
				coverTrigger: true,
				hover: true,
				container: document.querySelector('body')
			}
			let moreOptionsDropdownInstance = M.Dropdown.init(this.$el.querySelector('.dropdown-trigger'), moreOptionsDropdownOptions)
		}
	}
</script>

<style>
	/* CSS */
</style>
