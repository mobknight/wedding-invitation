
<div class="content">
    <figure class="image is-3by2 animate__animated animate__fadeIn">
        <img src={main_photo} alt="John and Bobae"/>
    </figure>

    <h1 class="animate__animated animate__fadeInUp">이요한 + 김보배</h1>
    <p class="animate__animated animate__fadeInUp animate__delay-1s">2025년 5월 3일 토요일 오후 2시 40분</p>
    <p class="animate__animated animate__fadeInUp animate__delay-2s">건대 스타시티아트홀</p>
    <p class="animate__animated animate__fadeInUp animate__delay-3s" on:animationstart={runCounter}>D<strong>{days_sign}{dd}</strong></p>
</div>

<div class="share">
    <p class="animate__animated animate__fadeInUp animate__delay-4s">
    <button class="button" on:click={share}>
            모바일 청첩장 공유하기
    </button>
    </p>
</div>

<div class="content">
    
</div>


<footer class="footer has-background-white">
    <a href="{base}/unused">Move to movie background page</a>

    <div class="content has-text-centered animate__animated animate__fadeInUp animate__delay-5s">
        <p>
            Handmade by John Lee
        </p>
    </div>
</footer>

<script>
    // @ts-nocheck
    import main_photo from '$lib/images/paris-047.webp'
    import { base } from '$app/paths';

    const today = new Date().setHours(0, 0, 0);
    const d_day = new Date('2025-05-03');
    const days_sign = (d_day >= today) ? '-' : '+';
    const days_until = Math.abs(Math.floor((d_day - today) / (1000 * 60 * 60 * 24)));
    
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

</script>

<style>
    .animate__fadeInUp {
        --animate-delay: 0.7s;
    }

    .footer {
        font-family: 'Cafe24Lovingu';
    }

</style>