<script>
    import { closeModal } from "svelte-native"
    export let article

</script>

<frame>
<page>
    <scrollView>
        <stackLayout class="container">
            <label textWrap="true" class="h2 white">{article.title}</label>
            <label textWrap="true" class="primary white padding">{article.description}</label>
            <!--Her skal det komme en se mer link til hjemmesiden til artikkelen-->
            <image
                class="img-rounden"
                src="{article.urlToImage}"
                alt="Bilde"
                stretch="aspectFill"
                />
            <label textWrap="true" class="body white">{"Skrevet av " + article.author}</label>
            <label textWrap="true" class="body white">{"Publisert " + article.publishedAt}</label>
            <button on:tap={ () => closeModal() } text="Tilbake" />
        </stackLayout>
    </scrollView> 
</page>
</frame>

<style>
    .padding {
        padding-bottom: 20;
        padding-top: 20;
    }
    .container {
        padding: 24;
        background-color: #555;
    }
    .white {
        color: white;
    }
</style>