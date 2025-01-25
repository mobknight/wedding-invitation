<article class="message is-primary animate__animated animate__fadeOut animate__delay-2s">
    <div class="message-body">
        <slot />
    </div>
</article>

<script>
    import { createEventDispatcher, onMount } from 'svelte';

    const dispatch = createEventDispatcher();

    onMount(() => {
        setTimeout(() => {
            dispatch("disappear");
        }, 2500);
    })
</script>

<style>
    .message {
        position: fixed;
        top: calc(100% - 8rem);
        left: calc(50% - 150px);
        width: 300px;
        height: auto;
    }

    .message-body {
        opacity: 0.8;
    }
</style>