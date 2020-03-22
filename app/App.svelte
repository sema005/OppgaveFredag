<script>
    import { Template } from "svelte-native/components"
    import { showModal } from "svelte-native"
    import { onMount } from "svelte"
    import Article from "./components/Article.svelte"

    const api_key = "edd201f109534dafa6d108db0929c7a8" //Min api key

    let articles = []

    // Henter nettsiden og legger api i arrayet "news"
    onMount( () => {
        fetch(`https://newsapi.org/v2/top-headlines?country=no&category=technology&apiKey=${api_key}`)
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
    <actionbar style="background-color:#333" class="white" title="Tech news" />
    <scrollView>
        <stackLayout class="articles">
        {#each articles as article}
            <flexboxLayout on:tap={() => showNews(article)} flexDirection="column" height="350" class="article" >
                <image src="{article.urlToImage}" width="300" height="200" class="img-rounded" stretch="aspectFill" alt="cover" />
                <label textWrap="true" class="h2 white" text="{article.title}"/>
            </flexboxLayout>
        {:else}
            <activityIndicator busy="{true}" />
        {/each}
        </stackLayout>
    </scrollView>
</page>


<style>
    page {
        width: 100%;
        background-color: black;
    }

    .articles {
        padding: 30;
        background-color: #333;
    }
    .article {
        padding: 10;
    }
    .white {
        color: white;
    }
</style>


