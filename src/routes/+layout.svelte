


<div class="container is-max-desktop has-background-white has-text-centered">
    <div class="has-background-white bg"></div>
    <slot />

    <div class="invisible-footer"></div>
</div>


<div class="tabs is-fullwidth is-small has-background-link main_menu">
    <ul>
        <!-- <li class="{$page.url.pathname === '/' ? 'has-background-primary has-text-black' : ''}"> -->
        <li>
            <a href="{base}/">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiHomeHeart} size=48></SvgIcon>
                </span>
            </a>
        </li>
        <li>
            <a href="{base}/map">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiMapClockOutline} size=48></SvgIcon>
                </span>
            </a>
        </li>
        <li>
            <a href="{base}/gallery">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiImageMultiple} size=48></SvgIcon>
                </span>
            </a>
        </li>
        <li>
            <a href="{base}/contact">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiCardAccountPhone} size=48></SvgIcon>
                </span>
            </a>
        </li>
        <li>
            <!-- svelte-ignore a11y-missing-attribute -->
            <a>
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <!-- svelte-ignore a11y-no-static-element-interactions -->
                <span class="icon is-medium share" on:click={share}>
                    <SvgIcon type="mdi" path={mdiShareVariantOutline} size=48></SvgIcon>
                </span>
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

    function share() {
        const target_url = 'https://mobknight.github.io/wedding-invitation'
        const title = '이요한/김보배의 결혼식에 초대합니다.'
        const text = '2025년 5월 3일 토요일 오후 2시 40분, 건대 스타시티아트홀'

        if (navigator.share) {
            navigator.share({
                title: title,
                text: text,
                url: target_url
            });
        } else {
            Kakao.Share.sendDefault({
                objectType: "feed",
                content: {
                    title: title,
                    description: text,
                    imageUrl: "https://mobknight.github.io/wedding-invitation/thumbnail.jpg",
                    link: {
                        mobileWebUrl: target_url,
                        webUrl: target_url,
                    }
                }
                
            });
        }
    }
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