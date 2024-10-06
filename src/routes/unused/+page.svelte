<!-- <div class="m-5">
    <video class="bg-video-content" autoplay muted loop defaultmuted playsinline preload='auto'>
        <source src={bg_movie} type="video/mp4" />
    </video>
</div>

<script>
    import bg_movie from '$lib/movies/bg.mp4'
</script> -->
<div class="block p-5">
    갤러리
    <div class="grid">
        {#each gallery as image}
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="box">
            <div class="cell" on:click={galleryClickHandler(image)}>
                <figure class="image is-128x128 is-flex is-align-items-center is-justify-content-center">
                    <img src="{image}" alt="John and Bobae" style="width:auto; height:auto; max-width: 100%; max-height: 100%" />
                </figure>
            </div>
        </div>
        {/each}
    </div>
</div>

<div class="modal {modal_active ? 'is-active' : ''}">
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div class="modal-background" on:click={() => {modal_active = false}}></div>
    <div class="modal-content" use:swipe={{ timeframe: 300 }} on:swipe={swipeHandler}>
        <p class="image">
            {#key selected_image}
                <img transition:fade={fade_params} src="{selected_image}" alt="" draggable="false"/>
            {/key}
        </p>
    </div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <button class="modal-close is-large" aria-label="close" on:click={() => {modal_active = false}}></button>
</div>



<script>
// @ts-nocheck
    import { swipe } from 'svelte-gestures';
    import { quintOut } from 'svelte/easing';
    import { fade } from 'svelte/transition';

    const images = import.meta.glob("$lib/gallery/*.jpg");

    let gallery = [];

    for (const path in images) {
        images[path]().then((url) => {
            gallery = [...gallery, path]
        });
    }

    let selected_image;
    let modal_active = false;
    let fade_params = {
        delay: 60,
        duration: 350,
        // easing: quintOut,
    }
    
    function galleryClickHandler(image) {
        selected_image = image;
        modal_active = true;
    }

    function swipeHandler(event) {
        
        const direction = event.detail.direction;
        const idx = gallery.indexOf(selected_image);

        if (direction === 'right') {
            const new_idx = idx - 1;
            if (new_idx >= 0) {
                selected_image = gallery[new_idx];
            }
        } else if (direction === 'left') {
            const new_idx = idx + 1;
            if (new_idx <= gallery.length) {
                selected_image = gallery[new_idx];
            }
        }
    }
</script>