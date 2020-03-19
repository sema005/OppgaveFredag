<script>
    import { Template } from "svelte-native/components"
    import { showModal } from "svelte-native"
    import { onMount } from "svelte"
    import Article from "./components/Article.svelte"

    const api_key = "edd201f109534dafa6d108db0929c7a8" //Min api key

    let articles = []

    // Henter nettsiden og legger api i arrayet "news"
    onMount( () => {
        fetch(`http://newsapi.org/v2/top-headlines?country=no&category=technology&apiKey=${api_key}`)
        .then( response => response.json() )
        .then( json => {
            console.log("Resultater")
            articles = json.articles
        }
        ).catch((err) => console.log(err))
    } )

    // Når man trykker på en artikkel så skal du få mer informasjon om nyheten
    const showNews = async (article) => {
        await showModal(
            {
                page: Article,
                props:{
                    article:article
                }
            }
        )
    }
</script>

<page>
    <actionbar style="background-color:#333" class="white" title="Norske nyheter" />
    <scrollView>
        <stackLayout class="articles">
        {#each articles as article}
            <flexboxLayout on:tap={() => showNews(article)} flexDirection="column" height="300" class="book article" >
                <image src="{article.urlToImage}" width="300" height="200" class="img-rounded" stretch="aspectFill" alt="cover" />
                <label textWrap="true" class="h4 white text-center text-primary" text="{article.title}"/>
            </flexboxLayout>
        {:else}
            <activityIndicator busy="{true}" />
        {/each}
        </stackLayout>
    </scrollView>
</page>

<!--
<style>
    page {
        width: 100%;
        background-color: black;
    }

    .nyheter {
        padding: 30;
        background-color: #555;
    }
    .nyhet {
        padding: 20;
        background-color: #777;

    }
</style>

<script>
    import { onMount } from 'svelte'
    import { showModal } from 'svelte-native'
    import Article from './modals/Article.svelte'
    const api_key = ''
    const url = `https://newsapi.org/v2/top-headlines?country=no&apiKey=${api_key}`
    let articles = []
    onMount(() => {
        fetch(url)
            .then( response => response.json() )
            .then( json => {
                articles = json.articles
            })
            .catch( error => console.log(error) )
    })
    const showArticle = async (article) => {
        await showModal(
            {
                page: Article,
                props:{
                    article:article
                }
            }
        )
    }
</script>

<page>
    <actionBar title="World News" />
    <stackLayout>
        <scrollView>
            <stackLayout class='articles'>            
                {#each articles as article}
                    <stackLayout
                        on:tap={ () => showArticle(article)} 
                        class='article'>
                    <image class='img-rounded' src='{article.urlToImage}' alt='cover' stretch='aspectFill' />
                    <label textWrap="{false}" class='h2 text-center white' text='{article.title}' />
                    <label class='body' text='{article.author}'/>
                    </stackLayout>
                {:else}
                    <activityIndicator busy={true} />
                {/each}
            </stackLayout>
        </scrollView>
    </stackLayout>
</page>

-->
<style>
    page{
        width:100%;
        background-color: black;
    }
    .article{
        padding: 24;
        animation:leftIn .4s ease;
    }
    .white{
        color:white;
    }
</style>