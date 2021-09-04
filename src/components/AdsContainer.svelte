<script>
    import SearchWrapper from './SearchWrapper.svelte';
    import ads from '../json/ads.json';
    import phonepic from '../img/nord.jpg';

    // let allAds = JSON.stringify(ads);
    let ad = 0;
    let allAds = ads.ads;

    // Load more ads below the default line, AJAX kind of :)
    function loadData(){
        const template = document.querySelector('.ads__wrapper');

        allAds.forEach(element => {
            const adTemplate = `
            <div class="ads__wrapper--one">
                <div class="ad__img">
                    <img src="/dist/img/nord.jpg" alt="Oneplus Nord">
                </div> 
                <div class="ad__details">
                    <h2 class="ad__details--title">${element.title}</h2>
                    <h4 class="ad__details--price">$${element.price}</h4>
                    <p class="ad__details--desc">${element.description}</p>
                </div>
            </div>
            `;
            template.innerHTML += adTemplate;
        });
    }

</script>
<style lang="scss">
    .row{
        width: 100%;
        max-width: 1440px;
        margin: 0 auto;
    }
    .ads__wrapper{
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 8px;
        margin-bottom: 2em;
        &--one{
            display: flex;
            //background-color: rgb(252, 241, 227);
            padding: .5em;
            border-radius: 5px;
            border: 2px solid burlywood;
            cursor: pointer;
            img{
                width: 80%;
            }
        }
    }
    .ad__img{
        width: 40%;
        img{
            width: 100%;
            height: auto;
        }
    }
    .ad__details{
        width: 60%;
        &--desc{
            font-weight: 300;
        }
        &--title{
            margin-top: 0;
        }
    }
    .load__button{
        text-align: center;
        button{
            padding: 1em 5em;
            cursor: pointer;
            text-transform: uppercase;
            border: .5px solid #000;
            // font-weight: 100;
            transition: ease-in-out 0.2s;
            border-radius: 5px;
            color: #000;
            &:hover{
                background-color: burlywood;
                color: #fff;
            }
        }
    }
    @media(max-width:768px){
        .ads__wrapper{
            display: grid;
            grid-template-columns: 1fr;
        }
    }
</style>
<SearchWrapper/>
<div class="ads__container row">
    <div class="ads__wrapper row">
    {#each allAds as ad}
    <div class="ads__wrapper--one">
        <div class="ad__img">
            <img src={phonepic} alt="Oneplus Nord">
        </div>
        <div class="ad__details">
            <h2 class="ad__details--title">{ad.title}</h2>
            <h4 class="ad__details--price">${ad.price}</h4>
            <p class="ad__details--desc">{ad.description}</p>
        </div>
    </div>
    {/each}
    </div>
    <div class="load__button row">
        <button on:click={loadData}>Load More</button>
    </div>
</div>