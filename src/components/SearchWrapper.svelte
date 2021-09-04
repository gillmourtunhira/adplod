<script>
    
    // Filter Ads
    //const filterAd

    let name = '';

    const filterAd = (name) => {
        const adWrapper = document.querySelector('.ads__wrapper')

        Array.from(adWrapper.children)
        .filter((ad) => !ad.textContent.includes(name) )
        .forEach((ad) => ad.classList.add('filtered') )
    }

    function getSearchedAdTitle(name){
        console.log(name)

        filterAd(name)
    }
    
</script>
<style lang="scss">
    .filtered{
        display: none;
    }
    .heading{
        width: 100%;
    }
    h1{
        text-align: center;
        font-weight: 300;
        padding: .5em 1em;
    }
    .search__ad{
        //margin: 2em 0;
        width: 100%;
        padding: 1em 5em;
        text-align: center;
        background-color:burlywood;
        margin-bottom: 1em;
        input{
            width: 82%;
            margin: 0 auto;
            height: 3em;
            padding: .2em 1em;
            border: 2px solid #fff;
            background-color: rgba(253, 240, 224, 0.733);
            outline: none;
            border-radius: 10px;
            font-size: medium;
        }
    }
</style>
<div class="search__ad">
    <div class="heading">
        <h1>Load Ads On Click</h1>
    </div>
    <form id="searchAds">
        <input on:keyup={getSearchedAdTitle(name)}  bind:value={name}  type="text" name="searchAd" placeholder="Search here...">
    </form>
    <h4>You searched for: {name}</h4>
</div>