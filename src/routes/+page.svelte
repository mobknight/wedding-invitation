<svelte:head>
    <meta property="og:type" content="website" />
    <meta property="og:title" content="이요한/김보배의 결혼식에 초대합니다." />
    <meta property="og:description" content="2025년 5월 3일 오후 2시, 건대 스타시티아트홀" />
    <meta property="og:image" content="{assets}/thumbnail.jpg" />
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
        
    </div>
</section>

<script>
    import { assets } from '$app/paths';
    import main_photo from '$lib/images/paris-047.png'
</script>