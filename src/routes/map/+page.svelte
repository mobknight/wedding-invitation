<svelte:head>
    <script type="text/javascript" src="https://oapi.map.naver.com/openapi/v3/maps.js?ncpClientId=ijycvnx5y2" on:load={() => {loaded = true}}></script>
</svelte:head>


{#if loaded}
    <div class="cotainer p-5">
        <div class="animate__animated animate__fadeInDown" id="map" style="width: 100%; height: 400px;"></div>
    </div>
{/if}


<a class="button" href="https://naver.me/FO9ftPQv" target="_blank">
    <figure class="image is-64x64">
        <img src={naver_map_icon} alt=""/>
    </figure>
</a>

<a class="button" href="https://tmap.life/f871c0f5" target="_blank">
    <figure class="image is-64x64">
        <img src={tmap_icon} alt=""/>
    </figure>
</a>
        
        

<script>
    //@ts-nocheck
    import { tick } from 'svelte'
    import tmap_icon from '$lib/images/tmap.svg'
    import naver_map_icon from '$lib/images/naver_map.webp'

    let loaded = false;
    let map;
    let marker;
    let infoWindow;

    $: {
        if (loaded == true) {
            drawMap();
        }
    }

    // 배포시 네이버 클라우드 콘솔에서 접근 가능한 URL 주소 추가할 것.

    async function drawMap() {
        await tick();
        console.log('Tick complete. Requesting Map');
        
        map = new naver.maps.Map('map', {
                center: new naver.maps.LatLng(37.5408014, 127.071374),
        });

        marker = new naver.maps.Marker({
            position: new naver.maps.LatLng(37.5408014, 127.071374),
            map: map,
            animation: naver.maps.Animation.BOUNCE
        });

        let contentString = [
            '<div class="iw_inner"><div class="box"><div class="content">',
            '   <h5>스타시티아트홀</h5>',
            '   <p>서울 광진구 능동로 110 스타시티 영존 5층<p>',
            '   <a href="https://starcityarthall.com/36" target="_blank">https://startcityhall.com</a>',
            '</div><div><div>'
        ].join('');

        infoWindow = new naver.maps.InfoWindow({
            content: contentString
        });

        naver.maps.Event.addListener(marker, "click", function(e) {
            if (infoWindow.getMap()) {
                infoWindow.close();
            } else {
                infoWindow.open(map, marker);
            }
        })
    }

</script>