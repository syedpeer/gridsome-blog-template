<template>
	<div class="layout d-flex flex-column h-100">
		<header class="header">
			<nav
				class="navbar fixed-top navbar-expand-md navbar-light bg-white shadow-sm"
			>
				<div class="container">
					<g-link class="navbar-brand" to="/" exact>
						{{ $static.metaData.siteName }}
					</g-link>

					<button
						class="navbar-toggler btn btn-sm"
						type="button"
						@click="toggleCollapse()"
					>
						<FaIcon v-if="!this.isMenuCollapsed" icon="bars" />
						<FaIcon v-if="this.isMenuCollapsed" icon="times" />
					</button>
					<div
						:class="{ show: isMenuCollapsed }"
						class="collapse navbar-collapse mt-2 mt-md-0 justify-content-end"
					>
						<ul class="navbar-nav">
							<li class="nav-item">
								<g-link class="nav-link" to="/" exact>
									Home
								</g-link>
							</li>
							<li class="nav-item">
								<g-link
									class="nav-link"
									to="/about"
									exact
								>
									About
								</g-link>
							</li>
						</ul>
					</div>
				</div>
			</nav>
		</header>

		<transition name="expand" appear>
			<main>
				<slot />
			</main>
		</transition>

		<Footer />
	</div>
</template>

<script>
    import FaIcon from '../components/Fa';
    import Footer from '../components/Footer';
    export default {
    	components: { FaIcon, Footer },
    	data: () => {
    		return {
    			isMenuCollapsed: false
    		};
    	},
    	methods: {
    		toggleCollapse() {
    			this.isMenuCollapsed = !this.isMenuCollapsed;
    		}
    	}
    };
</script>

<style lang="scss">
    $enable-shadows: true;
    @import '../assets/styles/custom-bootstrap';
    // @import '~bootstrap/scss/bootstrap';

    body {
    	padding-top: 58px;
    	background-color: theme-color('light');
    }

    .expand-enter-active,
    .expand-leave-active {
    	transition: opacity 1s;
    }

    .expand-enter,
    .expand-leave-to {
    	opacity: 0;
    }

    .card {
    	border-color: white;
    }

    .container {
    	.card {
    		margin-bottom: 20px;

    		h2 {
    			font-size: 1.5rem;
    			font-weight: 300;
    			line-height: 1.2;
    			margin-top: 20px;
    		}
    	}
    }

    .display-3 {
    	font-size: 3.5rem;
    }

    .display-4 {
    	font-size: 2rem;
    }

    @media (max-width: 480px) {
    	.container {
    		padding: 0;
    	}
    }
</style>

<static-query>
	query {
		metaData {
			siteName
		}
	}
</static-query>
