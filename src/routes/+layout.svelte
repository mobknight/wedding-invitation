
<div class="has-background-white bg">

</div>

<div class="has-background-white has-text-centered">
    <slot />

    <div class="invisible-footer"></div>
</div>


<div class="tabs is-fullwidth is-medium has-background-link main_menu">
    <ul>
        <!-- <li class="{$page.url.pathname === '/' ? 'has-background-primary has-text-black' : ''}"> -->
        <li>
            <a href="/">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiHomeHeart} size=48></SvgIcon>
                </span>
            </a>
        </li>
        <li>
            <a href="/map">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiMapClockOutline} size=48></SvgIcon>
                </span>
            </a>
        </li>
        <li>
            <a href="/gallery">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiImageMultiple} size=48></SvgIcon>
                </span>
            </a>
        </li>
        <li>
            <a href="/contact">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiCardAccountPhone} size=48></SvgIcon>
                </span>
            </a>
        </li>
    </ul>
</div>



<script>
// @ts-nocheck
    import SvgIcon from '@jamescoyle/svelte-icon';
    import { mdiHomeHeart, mdiMapClockOutline, mdiImageMultiple, mdiCardAccountPhone } from '@mdi/js';
    import { page } from '$app/stores';
</script>

<style>
    .main_menu {
        position: fixed;
        height: 4rem;
        top: calc(100% - 4rem);
        width: 100%;
        z-index: 10;
    }

    .invisible-footer {
        height: 4rem;
    }

    .bg {
        position: fixed;
        height: 100%;
        width: 100%;
        top: 0;
        left: 0;
        z-index: -1;
    }
</style>