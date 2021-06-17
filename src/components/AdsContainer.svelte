<script>
    import ads from '../json/ads.json';
    import phonepic from '../img/nord.jpg';

    // let allAds = JSON.stringify(ads);
    let ad = 0;
    let allAds = ads.ads;

    // Load more ads below the default line, AJAX kind of :)
    function loadData(){
        const template = document.querySelector('.ads__wrapper');

        allAds.forEach(element => {
            let divWrapperOne = document.createElement('div');
            divWrapperOne.classList = 'ads__wrapper--one svelte-1f7uzap'

            // Details Div
            let divDetails = document.createElement('div');
            let h2Title = document.createElement('h2');
            let h4Price = document.createElement('h4');
            let pDesc = document.createElement('p');

            // Add classes
            divDetails.classList = 'ad__details svelte-1f7uzap';
            h2Title.classList = 'ad__details--title svelte-1f7uzap';
            h4Price.classList = 'ad__details--price svelte-1f7uzap';
            pDesc.classList = 'ad__details--desc svelte-1f7uzap';

            h2Title.innerText = element.title;
            h4Price.innerText = element.price;
            pDesc.innerText = element.description;
            // Append Children
            divDetails.appendChild(h2Title);
            divDetails.appendChild(h4Price);
            divDetails.appendChild(pDesc);

            divWrapperOne.appendChild(divDetails);
            template.appendChild(divWrapperOne);
        });
    }

    let name = '';
    // Search ad typed in the input form
    function filterAds(name){
        console.log(name)
    }


</script>
<style lang="scss">
    .row{
        width: 100%;
        max-width: 1440px;
        margin: 0 auto;
    }
    .search__ad{
        margin: 2em 0;
        width: 100%;
        input{
            width: 100%;
            height: 3em;
            padding: .2em 1em;
            border: none;
            background-color: rgba(253, 240, 224, 0.733);
            outline: none;
            border-radius: 10px;
            font-size: medium;
        }
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
<div class="ads__container row">
    <div class="search__ad">
        <input on:input={filterAds}  bind:value={name}  type="text" placeholder="Search here...">
        <h4>You search for: {name}</h4>
    </div>
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