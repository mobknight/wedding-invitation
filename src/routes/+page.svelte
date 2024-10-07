<svelte:head>
    <meta property="og:type" content="website" />
    <meta property="og:title" content="이요한/김보배의 결혼식에 초대합니다." />
    <meta property="og:description" content="2025년 5월 3일 오후 2시, 건대 스타시티아트홀" />
    <meta property="og:image" content="https://mobknight.github.io/wedding-invitation/thumbnail.jpg" />
</svelte:head>


<section class="hero">
    <div class="hero-body">
        <div class="block ml-5 mr-5">
            <figure class="image animate__animated animate__fadeInDown">
                <img src={main_photo} alt="John and Bobae"/>
            </figure>
        </div>

        <p class="title">이요한 + 김보배</p>
        <p>2025년 5월 3일 토요일 오후 2시</p>
        <p>건대 스타시티아트홀</p>

        <p>D<strong>{days_sign}{days_until}</strong>일</p>
        
    </div>
</section>

<script>
    // @ts-nocheck
    import main_photo from '$lib/images/paris-047.png'

    const today = new Date().setHours(0, 0, 0);
    const d_day = new Date('2025-05-03');
    const days_sign = (d_day >= today) ? '-' : '+';
    const days_until = Math.abs(Math.floor((d_day - today) / (1000 * 60 * 60 * 24)));
    

</script>