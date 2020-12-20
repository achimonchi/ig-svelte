<script>
    export let image = "/img/default.png";
    export let like = 33;
    export let comment = 23;
</script>

<div class="card-ui">
    <div class="ket">
        <div class="like">
             <p><i class="fas fa-heart"></i><span>{like}</span></p>
        </div>
        <div class="comment">
            <p><i class="fas fa-fw fa-comment"></i><span>{comment}</span></p>
        </div>
     </div>
    <div class="img">
        <img src="{image}" alt="">
    </div>
    
</div>

<style>
    .card-ui .img img{
        width: 100%;
        /* background-position-x: center;
        background-position-y: center; */
        transition: .3s ease-in-out;
    }

    .card-ui .img{
        z-index: -1;
        background-color: #000;
        /* position: absolute; */
    }

    .card-ui .img img{
        z-index: -2;
    }

    .card-ui:hover .img img{
        opacity: .5;
    }

    .card-ui:hover .ket{
        opacity: 1;
    }

    .card-ui .ket{
        transition: .2s ease-in-out;
        opacity: 0;
        z-index: 999;
        color: white;
        display: flex;
        position: absolute;
        flex-direction: row;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        /* margin-top: -15vh; */
    }

    .card-ui .ket div{
        margin-left: 20px;
        margin-right: 20px;
    }
</style>