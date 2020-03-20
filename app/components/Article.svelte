<script>
    import { closeModal } from "svelte-native"
    export let article

</script>

<frame>
<page>
    <scrollView>
        <stackLayout style="padding:24">
            <label textWrap="true" class="h2">{article.title}</label>
            <label textWrap="true" class="primary padding">{article.description}</label>
            <!--Her skal det komme en se mer link til hjemmesiden til artikkelen-->
            <image
                class="img-rounden"
                src="{article.urlToImage}"
                alt="Bilde"
                stretch="aspectFill"
                />
            <label textWrap="true" class="body">{"Skrevet av " + article.author}</label>
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
</style>