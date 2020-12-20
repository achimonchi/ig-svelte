<script>
    export let id;
    import {params} from '@sveltech/routify';
    import { Col, Container, Row } from 'sveltestrap';
    
    let visible = false;
    const url = `https://www.instagram.com/p/${$params.id}/?__a=1`;
    const fetchData = async(url) =>{
        const postData = await fetch(url);
        const f = await postData.json();
        console.log(f.graphql.shortcode_media);
        visible = true;
        return f.graphql.shortcode_media;
    }
    $: post = fetchData(url);


    import { fly } from 'svelte/transition';
    
</script>

<main>
    {#await post}
        <Container class="mt-5">
            <Row>
                <Col>
                    <h5 class="text-center">Loading ...</h5>
                </Col>
            </Row>
        </Container>
    {:then p } 
        {#if visible == true}
            <div in:fly="{{ y: 100, duration: 500 }}">
                <Container class="mt-5">
                    <Row>
                        <Col md="6" class="mb-3">
                            <img class="img-ig" src="{p.display_url}" alt="">
                        </Col>
                        <Col md="6">
                            <h3><b>{p.owner.username}</b></h3>
                            <br>
                            <h6>{p.edge_media_to_caption.edges[0].node.text}</h6>
                            <br>
                            <a href="/" class="btn btn-block btn-dark float-right btn-sm text-white">Kembali</a>                    
                        </Col>
                    </Row>
                </Container>        
            </div>
        {/if}
    {/await}
</main>

<style>
    .img-ig{
        width: 100%;
        border-radius: 8px;
        box-shadow: 0px 20px 30px -10px rgba(0,0,0,.3);
    }

    main{
        max-width: 960px;
        margin:auto;
    }
</style>