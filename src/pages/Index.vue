<template>
	<Layout>
		<div class="container pt-4 pb-4">
			<!-- TODO - AUTHOR -->
			<div
				class="d-flex align-items-center justify-content-center text-center"
				style="height: 380px;"
			>
				<div
					class="d-flex flex-column align-items-center justify-items-center pt-4 pb-4"
				>
					<div>
						<g-image
							width="180"
							src="~/assets/images/author.png"
							class="rounded-circle"
						/>
					</div>
					<h1 class="display-4">{{ $page.metaData.siteName }}</h1>
					<p>{{ $page.metaData.siteDescription }}</p>
				</div>
			</div>

			<!-- TODO- Pagination? -->
			<div class="posts">
				<PostCard v-for="post of posts" :key="post.id" :post="post" />
			</div>
		</div>
	</Layout>
</template>

<script>
    import { PostModel } from '../models/post.model';
    import PostCard from '../components/PostCard';

    export default {
    	components: { PostCard },
    	metaInfo: {
    		title: 'Home'
    	},
    	computed: {
    		posts: function() {
    			return this.$page
    				? this.$page.allPost.edges.map(e => new PostModel(e.node))
    				: [];
    		}
    	}
    };
</script>

<page-query>
{
  	allPost {
		totalCount
		pageInfo {
			totalPages
			currentPage
		}
		edges {
			node {
				id
				title
				path
				excerpt
				date (format:"DD.MM.YYYY")
				tags {
					title
					path
				}
				author {
					name
				}
				category {
					title
				}
			}
		}
  	}

	metaData {
		siteName
		siteDescription
	}
}
</page-query>
