<script>
	import Header from './../components/Header.svelte';
	import Footer from './../components/Footer.svelte';
	import Card from './../components/Card.svelte';
    import axios from 'axios';

    import {url} from '@sveltech/routify';
    
    import {Container, Row, Col} from 'sveltestrap';

	let posts = [];
	let username = "";
    let isLoading = false;

	const onClickSearch=async (e)=>{
		username = e.detail;
		isLoading = true;
		try{
			const uri = `https://www.instagram.com/${username}/?__a=1`;
			const f = await fetch(uri);
			const graphData = await f.json();	
			console.log(!f ? true : false);
			const user = graphData.graphql.user;
			const userPost = user.edge_owner_to_timeline_media;
			posts= userPost.edges;
			console.log(posts);
			isLoading = false;
		} catch(err){
			isLoading = false;
			posts = [];
		}
    }

    // animation
    import { fly, fade } from 'svelte/transition';
</script>


<Header {username} on:onClickSearch={onClickSearch} />
<main in:fade={{duration:500}}>
	<Container>
		<Row class="justify-content-center">
			{#if posts.length > 0}
				{#if isLoading === false}
                    {#each posts as p,i}
                        <div class="col-md-4 mb-3" in:fly={{y:200, duration:300*i}}>
                            <a href={$url('post/:id', {id : p.node.shortcode})} >
                                <Card comment={p.node.edge_media_to_comment.count} like={p.node.edge_liked_by.count} image={p.node.thumbnail_src}/>
                            </a>
                        </div>
					{/each}
				{:else}
					<Col md="8">
						<h3 class="text-center">Loading ...</h3>
					</Col>
				{/if}
			{:else}
				{#if isLoading === false}
				<Col md="8">
					<h3 class="text-center">Data Tidak Ditemukan</h3>
				</Col>
				{:else}
				<Col md="8">
					<h3 class="text-center">Loading ...</h3>
				</Col>
				{/if}
			{/if}

        </Row>
	</Container>
</main>

<Footer/>

<style>
	main{
		max-width: 960px;
		margin: auto;
	}
</style>