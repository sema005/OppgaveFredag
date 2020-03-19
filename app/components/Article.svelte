<script>
    import { closeModal } from "svelte-native"
    export let article

</script>

<frame>
<page>
    <scrollView>
        <stackLayout style="padding:24">
            <label textWrap="true" class="h2">{article.title}</label>
            <label textWrap="true" class="primary">{article.description}</label>
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


<!--
<script>
    import { closeModal } from 'svelte-native'
    export let article
</script>

<frame>
<page>
    <scrollView>
        <stackLayout style='padding:24'>
            <textField class='h1' text='{article.title}' />
            <textField class='primary' text='{article.author}' />
            <textView class='body' text='{article.description}' />
            <image 
                class='img-rounded'
                src='{article.urlToImage}'
                alt='article cover image'
                stretch='aspectFill'
                />
            <button on:tap={ () => closeModal() } text='close' />
        </stackLayout>
    </scrollView>
</page>
</frame>
-->