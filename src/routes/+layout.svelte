
<div class="container is-max-desktop has-background-white has-text-centered">
    <div class="has-background-white bg"></div>
    <slot />

    <div class="invisible-footer"></div>
</div>

<div class="tabs is-fullwidth is-small {$page.url.pathname.substr($page.url.pathname.lastIndexOf('/')) === '/' ? '' : 'has-background-white'} main_menu" style="{$page.url.pathname.substr($page.url.pathname.lastIndexOf('/')) === '/' ? 'background: linear-gradient(transparent, #01070A);' : ''}">
    <ul>
        <!-- <li class="{$page.url.pathname === '/' ? 'has-background-primary has-text-black' : ''}"> -->
        <li>
            <a href="{base}/" class="{$page.url.pathname.substr($page.url.pathname.lastIndexOf('/')) === '/' ? 'has-text-link' : 'has-text-grey-dark'}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiHomeHeart} size=48></SvgIcon>
                </span>
                <span>홈</span>
            </a>
        </li>
        <li>
            <a href="{base}/map" class="{$page.url.pathname.substr($page.url.pathname.lastIndexOf('/')) === '/' ? 'has-text-link' : 'has-text-grey-dark'}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiMapClockOutline} size=48></SvgIcon>
                </span>
                <span>위치</span>
            </a>
        </li>
        <li>
            <a href="{base}/gallery" class="{$page.url.pathname.substr($page.url.pathname.lastIndexOf('/')) === '/' ? 'has-text-link' : 'has-text-grey-dark'}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiImageMultiple} size=48></SvgIcon>
                </span>
                <span>사진</span>
            </a>
        </li>
        <li>
            <a href="{base}/contact" class="{$page.url.pathname.substr($page.url.pathname.lastIndexOf('/')) === '/' ? 'has-text-link' : 'has-text-grey-dark'}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiCardAccountPhone} size=48></SvgIcon>
                </span>
                <span>연락</span>
            </a>
        </li>
    </ul>
</div>



<script>
// @ts-nocheck
    import SvgIcon from '@jamescoyle/svelte-icon';
    import { mdiHomeHeart, mdiMapClockOutline, mdiImageMultiple, mdiCardAccountPhone, mdiShareVariantOutline } from '@mdi/js';
    import { page } from '$app/stores';
    import { base } from '$app/paths';

    import('https://t1.kakaocdn.net/kakao_js_sdk/2.7.2/kakao.min.js').then((sdk) => {
        Kakao.init('05f251792f6c66dc1711334f4f179773');
    });

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