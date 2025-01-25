<div class="container p-5 is-fullwidth animate__animated animate__slideInDown">
    <swiper-container
        class="gallery-main"
        thumbs-swiper=".gallery-thumbs"
        slides-per-view={1}
        space-between={1}
        lazy-preload-prev-next={1}
        breakPoints={{
            1024: {
                slidesPerView: 3,
            }
        }}
    >
        {#each gallery as image}
            <swiper-slide>
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
                <figure class="image is-2by3 main-picture is-flex is-align-items-center is-justify-content-center" on:click={() => {galleryClickHandler(image)}}>
                    <enhanced:img src="{image}" alt="John and Bobae" style="object-fit: scale-down;" loading="lazy"/>
                </figure>
                <div class="swiper-lazy-preloader"></div>
            </swiper-slide>
        {/each}
    </swiper-container>
</div>

<div class="container pt-2 pr-5 pl-5 pb-2 thumbs has-background-white animate__animated animate__slideInUp">
    <swiper-container
        class="gallery-thumbs"
        slides-per-view={5}
        space-between={10}
        centered-slides={true}
        watch-slides-visibility={true}
        watch-slides-progress={true}
        free-mode={true}
        lazy-preload-prev-next={5}
        breakpoints={{
            1024: {
                slidesPerView: 11,
            }
        }}
        >

        {#each gallery as image}
            <swiper-slide>
                <figure class="image is-square">
                    <enhanced:img src="{image}" alt="John and Bobae" loading="lazy"/>
                </figure>
                <div class="swiper-lazy-preloader"></div>
            </swiper-slide>
        {/each}

    </swiper-container>
</div>

<div class="modal {modal_active ? 'is-active' : ''}">
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div class="modal-background" on:click={() => {modal_active = false}}></div>
    <div class="modal-content">
        <p class="image">
            {#if selected_image}
                <enhanced:img src="{selected_image}" alt="" draggable="false"/>
            {/if}
        </p>
    </div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <button class="modal-close is-large" aria-label="close" on:click={() => {modal_active = false}}></button>
</div>


<script>
    //@ts-nocheck
    const images = import.meta.glob("$lib/gallery/*.jpg", {
        eager: true,
        query: {
            enhanced: true
        }
    });

    let gallery = [];

    Object.values(images).forEach((v) => {
        gallery = [...gallery, v.default];
    })

    // Swiper!
    import { register } from 'swiper/element/bundle'
    register();
    
    let modal_active;
    let selected_image;

    function galleryClickHandler(image) {
        selected_image = image;
        modal_active = true;
    }
</script>

<style>
    :global(.gallery-thumbs .swiper-slide-thumb-active) {
        opacity: 0.2;
    }

    .thumbs {
        position: fixed;
        top: calc(100% - 4rem - 64px - 1rem);
        z-index: 5;
    }

    .main-picture {
        width: auto;
        height: auto;
        max-width: 100%;
        max-height: 100%;
    }

</style>