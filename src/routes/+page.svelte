<script lang='ts'>
    import { goto } from "$app/navigation";


    export let data;
    console.log(data);

    const colorArray = ['blue-letter', 'red-letter', 'yellow-letter', 'blue-letter', 'green-letter', 'red-letter'];

    let logoString = 'Goggle';
    $: splitLogo = inputText.split('');

    $: splitTemplate = logoString.split('')
    
    let inputText = '';
    let inputElement: HTMLElement;

    // const changeLogo = () => {
    //     if (inputText.length) {
    //         logoString = inputText;
    //         inputText = ''
    //     }
    // }

    const enterPressed = (e: KeyboardEvent) => {
        if (e.key === 'Enter') inputText = '';
    }
</script>

<svelte:window on:keydown={enterPressed}/>

<main>

    <nav>
        <div id='nav-left'>
            <a href='https://www.google.com' target='_blank' rel='noreferrer'>About</a>
            <a href='https://www.google.com' target='_blank' rel='noreferrer'>Store</a>
        </div>
        <div id='nav-right'>
            <a href='https://www.google.com' target='_blank' rel='noreferrer'>Gmail</a>
            <a href='https://www.google.com' target='_blank' rel='noreferrer'>Images</a>
            <img src='https://upload.wikimedia.org/wikipedia/commons/b/b2/Hamburger_icon.svg' alt='Menu' style='cursor: pointer; height: 1.5em'>
            <div id='avatar'><span>C</span></div>
        </div>
    </nav>

<section id='main-content'>
    <p class='red-letter' style='font-weight: bold'>not google</p>
    <h1>
    {#if !inputText.length}
    {#each splitTemplate as character, i}
    <span class={colorArray[i % colorArray.length]}>{character === ' ' ? '_' : character}</span>
    {/each}
    {:else}
    {#each splitLogo as character, i}
    <span class={colorArray[i % colorArray.length]}>{character === ' ' ? '_' : character}</span>
    {/each}
    {/if}
    </h1>
    <div id='search-input' 
        on:click={() => inputElement.focus()} 
        on:keydown={() => inputElement.focus()}
        
        >
        <img 
            src='https://upload.wikimedia.org/wikipedia/commons/5/55/Magnifying_glass_icon.svg'
            alt='magnifying glass' 
        />
        <input 
            bind:value={inputText}
            bind:this={inputElement}
        />
    </div>
    
    <div id='input-buttons'>
        <button on:click={() => inputText=''}>Google Search</button>
        <button on:click={() => inputText=''}>I'm Feeling Lucky</button>
    </div>
</section>

<footer>
    <div id='footer-left'>
        <a href='https://www.google.com' target='_blank' rel='noreferrer'>Advertising</a>
        <a href='https://www.google.com' target='_blank' rel='noreferrer'>Business</a>
        <a href='https://www.google.com' target='_blank' rel='noreferrer'>How Search works</a>
    </div>
    <div id='footer-right'>
        <a href='https://www.google.com' target='_blank' rel='noreferrer'>Privacy</a>
        <a href='https://www.google.com' target='_blank' rel='noreferrer'>Terms</a>
        <a href='https://www.google.com' target='_blank' rel='noreferrer'>Settings</a>
    </div>
</footer>

</main>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
    
    :global(body) {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: 'Roboto', sans-serif;
    }

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        /* outline: 1px solid red; */
    }
    
    main {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    nav {
        display: flex;
        justify-content: space-between;
        padding: 20px;
        font-size: .9em;
    }

    #nav-left {
        display: flex;
        align-items: center;
        gap: 1em;
    }

    #nav-right {
        display: flex;
        gap: 1em;
        align-items: center;
    }

    #avatar {
        background-color: rgb(160, 160, 160);
        width: 30px;
        height: 30px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-inline: 1em;
        cursor: pointer;
    }

    a {
        text-decoration: none;
        color: black;
    }

    #main-content {
        text-align: center;
        flex: 1;
        margin-top: 3em;
    }

    h1 {
        font-size: 5em;
        min-height: 1.2em;
        overflow: hidden;
        margin-bottom: .4em;
    }

    #search-input {
        border: 1px solid red;
        margin-bottom: 2em;
        width: 35%;
        margin-inline: auto;
        border-radius: 20px;
        border: 1px solid rgba(200, 200, 200, 0.797);
        display: flex;
        align-items: center;
    }

    #search-input:hover {
        box-shadow: 0px 0px 2px grey;
    }

    img {
        height: 1em;
        /* position: relative;
        left: 0;
        top: 5px; */
        opacity: .5;
        margin-left: 10px;
    }

    input {
        padding: 10px;
        border: none;
        width: 90%;
        border-radius: 20px;
    }

    input:focus {
        outline: none;
    }

    button {
        background-color: rgb(246, 246, 246);
        border: none;
        cursor: pointer;
    }

    #input-buttons {
        display: flex;
        gap: 10px;
        justify-content: center;
        gap: 2em;
    }

    #input-buttons > button {
        padding: 10px;
        border-radius: 5px;
    }

    #input-buttons > button:hover {
        /* outline: 1px solid rgb(189, 189, 189); */
        box-shadow: 0px 0px 2px gray;
    }

    .blue-letter {
        color: rgba(0, 64, 255, 0.616);
    }

    .red-letter {
        color: rgba(228, 0, 0, 0.737);
    }

    .yellow-letter {
        color: rgb(255, 217, 0);
    }
    
    .green-letter {
        color: rgba(0, 128, 0, 0.648);
    }

    footer {
        display: flex;
        justify-content: space-between;
        background-color: rgba(128, 128, 128, 0.129);
        align-items: center;
        height: 4em;
        font-size: .9em;
        flex-direction: row;
        flex-wrap: wrap;
    }

    footer a {
        color: gray;
    }

    #footer-left {
        display: flex;
        gap: 1.5em;
        margin-left: 1em;
    }

    #footer-right {
        display: flex;
        gap: 1.5em;
        margin-right: 1em;
    }

</style>