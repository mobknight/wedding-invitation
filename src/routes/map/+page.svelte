<svelte:head>
    <script type="text/javascript" src="https://oapi.map.naver.com/openapi/v3/maps.js?ncpClientId=ijycvnx5y2" on:load={() => {loaded = true}}></script>
</svelte:head>

<div class="container p-5">

    <div class="content has-text-right is-large">
        2025년 5월 3일 토요일
        <p class="is-size-6">오후 2시</p>
    </div>
    

    <table class="table is-fullwidth has-background-white">
        <thead class="has-text-centered">
            <tr>
                <th>일</th>
                <th>월</th>
                <th>화</th>
                <th>수</th>
                <th>목</th>
                <th>금</th>
                <th>토</th>
            </tr>
        </thead>
        <tbody>
            {#each calendar_data as week}
                <tr>
                    {#each week as day}
                        {#if day === 3}
                            <td class="has-background-primary has-text-white">{day}</td>
                        {:else}
                            <td>{day}</td>
                        {/if}
                    {/each}
                </tr>
            {/each}
        </tbody>
    </table>
</div>

<div class="container p-5">
    <div class="content has-text-right is-large">
        스타시티아트홀
        <p class="is-size-6">서울 광진구 능동로 110 스타시티 영존 5층</p>
    </div>

    {#if loaded}
        <div id="map" style="width: 100%; height: 300px;"></div>
    {/if}

    <div class="p-3">
        <a class="button" href="https://kko.to/Kw91W2O8AF" style="background-color:#FAE100;" target="_blank">
            <figure class="image is-32x32">
                <img src={kakao_map_icon} alt=""/>
            </figure>
        </a>
        <a class="button" href="https://maps.app.goo.gl/hJ3aLVPu8kiC3N2q9" style="background-color:#FFFFFF;" target="_blank">
            <figure class="image is-32x32">
                <img src={google_map_icon} alt=""/>
            </figure>
        </a>
        
        <a class="button" href="https://naver.me/FO9ftPQv" style="background-color:#FFFFFF;" target="_blank">
            <figure class="image is-32x32">
                <img src={naver_map_icon} alt=""/>
            </figure>
        </a>
        <a class="button" href="https://tmap.life/f871c0f5" style="background-color:#FFFFFF;" target="_blank">
            <figure class="image is-32x32">
                <img src={tmap_icon} alt=""/>
            </figure>
        </a>
    </div>

    <div class="box has-background-white">
        <div class="content has-text-left">
            <h4>지하철</h4>
            <p>2호선 / 7호선 건대입구역 3번 출구 앞</p>
            <h4>버스</h4>
            <p>건대입구역, 건대입구역 사거리 하차</p>
            <ul>
                <li>
                    간선: 240, 721
                </li>
                <li>
                    지선: 2016, 2222, 3217, 3220, 4212
                </li>
                <li>
                    직행: 102, 3500
                </li>
                <li>
                    공항: 6013
                </li>
            </ul>
        </div>
    </div>
</div>

<!-- <hr> -->


        

<script>
    //@ts-nocheck
    import { tick } from 'svelte'
    import tmap_icon from '$lib/images/tmap.svg'
    import naver_map_icon from '$lib/images/naver_map.webp'
    import kakao_map_icon from '$lib/images/kakao_map.webp'
    import google_map_icon from '$lib/images/google_map.webp'

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
            '</div></div></div>'
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


    // Calendar

    const calendar_data = setCalendarSet(2025, 5, 3);
        
    function setCalendarSet(year, month, targetDate) {
        const numberOfDays = new Date(year, month, 0).getDate();
        let str_month;

        if (month.toString().length < 2) {
            str_month = '0' + month;
        } else {
            str_month = month.toString();
        }
        const firstDay = new Date(year + '-' + str_month + '-01');
        const firstDOW = firstDay.getDay();
                
        let currentDate = 1;

        let weeks = [[]];

        for (let i = 0; i < firstDOW; i++) {
            weeks[0].push('');
        }

        for (let i = firstDOW; i < 7; i++) {
            weeks[0].push(currentDate);
            currentDate++;
        }

        let newWeek = [];
        for (let i = currentDate; i <= numberOfDays; i++) {
            newWeek.push(currentDate);
            currentDate++;

            if (newWeek.length >= 7) {
                weeks.push(newWeek);
                newWeek = [];
            }
        }

        // put last week in, if any remaining days
        if (newWeek.length > 0) {
            for (let i = newWeek.length; i < 7; i++) {
                newWeek.push('');
            }
            weeks.push(newWeek);
        }
        
        return weeks;
    }

</script>

