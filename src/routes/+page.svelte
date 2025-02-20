<!-- <video class="bg-video-content" autoplay muted loop defaultmuted playsinline preload='auto'> -->
<!-- svelte-ignore a11y-media-has-caption -->
<video class="bg-video-content" autoplay loop playsinline muted={unmuted ? null : 'muted'} defaultmuted preload='auto' on:click={toggle_mute}>
    <source src={bg_movie} type="video/mp4" />
</video>

<div class="content has-text-white has-text-centered">
    <br>
    <p class="animate__animated animate__fadeInUp" on:animationstart={runCounter}>이요한 김보배 | D<strong class="has-text-white">{days_sign}{dd}</strong></p>
</div>

<div class="block" style="padding-right: 2rem;">
    <div class="content has-text-white has-text-right">
        <br>
        <h1 class="animate__animated animate__fadeInUp has-text-white">WEDDING<br>DAY</h1>
        <br><br>
        <p class="animate__animated animate__fadeInUp animate__delay-1s">2025년 5월 3일 토요일<br>오후 2시 40분</p>
        <p class="animate__animated animate__fadeInUp animate__delay-2s">건대 스타시티아트홀</p>
    </div>
</div>

<div class="share">
    <p class="animate__animated animate__fadeInUp animate__delay-3s">
    <button class="button" on:click={share}>
            청첩장 공유하기
    </button>
    </p>
</div>

<footer class="footer has-background-white handwritten">
    <div class="content has-text-centered animate__animated animate__fadeInUp animate__delay-4s">
        <p>
            Handmade by John Lee
        </p>
    </div>
</footer>


<script>
    // @ts-nocheck
    import bg_movie from '$lib/movies/bg.mp4'

    const today = new Date().setHours(0, 0, 0);
    const d_day = new Date('2025-05-03');
    const days_sign = (d_day >= today) ? '-' : '+';
    const days_until = Math.abs(Math.floor((d_day - today) / (1000 * 60 * 60 * 24)));
    
    let unmuted;

    let dd;
    // runCounter();

    function runCounter() {
        if (d_day >= today) {
            countDown(2764, days_until);
        } else {
            countUp(days_until);
        }
    }
    
    function countDown(from, to) {
        dd = from;
        const max = from - to;
        let now = max;

        const interval = setInterval(() => {

            dd = Math.ceil(from - (max - now)) - 1;

            if (now < 1) {
                clearInterval(interval)
            }

            const step = now / 10;
            now -= step;
        }, 40);
    }

    function countUp(to) {
        dd = 0;
        const max = to;
        let now = max;

        const interval = setInterval(() => {

            dd = Math.ceil(max - now);

            if (now < 1) {
                clearInterval(interval)
            }

            const step = now / 10;
            now -= step;
        }, 40);
    }

    
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

    function toggle_mute() {
        unmuted = !unmuted;
    }

</script>

<style>
    .animate__fadeInUp {
        --animate-delay: 0.7s;
    }

    .handwritten {
        font-family: 'Cafe24Lovingu';
    }

    .bg-video-content {
        left: 0;
        top: 0;
        min-width: 100%;
        min-height: 100%;
        position: absolute;
        z-index: 0;
    }

    .share {
        position: fixed;
        left: 2rem;
        top: calc(100% - 8rem);
    }

</style>