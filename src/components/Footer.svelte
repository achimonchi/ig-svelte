<script>
    import { scale} from 'svelte/transition';
</script>

<footer>
    <div class="copyright" in:scale={{duration:500}}>
        Copyright &copy; 2020 | <b>NooBeeID</b> 
    </div>
</footer>

<style>
    footer{
        padding: 20px;
        text-align: center;
    }
    .copyright{
        padding:20px;
        border-top: 5px solid #dadada;
        display: inline-block;
        font-size: .8em;
    }
</style>