<figure class="image is-3by2 animate__animated animate__fadeIn">
    <img src={main_photo} alt="John and Bobae"/>
</figure>

<div class="block pt-5">
    <div class="columns is-mobile">
        <!-- 신랑측 -->
        <div class="column is-half">
            <span class="is-size-5">신랑</span>
            <span class="is-size-4">이요한</span>
            <div class="content pt-4">
                <a href="tel://{phone_number_groom}" class="pr-2">
                    <span class="icon is-large">
                        <SvgIcon type="mdi" path={mdiPhone} size=48></SvgIcon>
                    </span>
                </a>
                <a href="sms://{phone_number_groom}">
                    <span class="icon is-large">
                        <SvgIcon type="mdi" path={mdiMessageProcessing} size=48></SvgIcon>
                    </span>
                </a>
            </div>
            <div class="content">
                <button class="button" on:click={() => {copyToClipboard('토스뱅크 1000-0610-6759')}}>계좌번호 복사</button>
            </div>
            <div class="content">
                <a class="button" href="https://link.kakaopay.com/_/fq5Dm59" target="_blank" style="background-color:#FAE100;">
                    <figure class="image">
                        <img src={kakaopay} alt="" style="height:1.5rem; width:4rem;"/>
                    </figure>
                </a>
            </div>
        </div>
        <!-- 신부측 -->
        <div class="column is-half">
            <span class="is-size-5">신부</span>
            <span class="is-size-4">김보배</span>
            <div class="content pt-4">
                <a href="tel://{phone_number_bride}" class="pr-2">
                    <span class="icon is-large">
                        <SvgIcon type="mdi" path={mdiPhone} size=48></SvgIcon>
                    </span>
                </a>
                <a href="sms://{phone_number_bride}">
                    <span class="icon is-large">
                        <SvgIcon type="mdi" path={mdiMessageProcessing} size=48></SvgIcon>
                    </span>
                </a>
            </div>
            <div class="content">
                <button class="button" on:click={() => {copyToClipboard('토스뱅크 1000-0740-3010')}}>계좌번호 복사</button>
            </div>
            <div class="content">
                <a class="button" href="https://link.kakaopay.com/_/yqJaIoR" target="_blank" style="background-color:#FAE100;">
                    <figure class="image">
                        <img src={kakaopay} alt="" style="height:1.5rem; width:4rem;"/>
                    </figure>
                </a>
            </div>
        </div>
    </div>
</div>


{#if show_message}
    <Message on:disappear={() => {show_message = false}}>
        {message}
    </Message>
{/if}

<script>
    // @ts-nocheck
    import SvgIcon from '@jamescoyle/svelte-icon';
    import { mdiPhone, mdiMessageProcessing, mdiInstagram } from '@mdi/js';
    import Message from '$lib/components/Message.svelte';
    import kakaopay from '$lib/images/kakaopay.svg'
    import main_photo from '$lib/images/paris-047.webp'

    const phone_number_groom = '010-3692-5521'
    const phone_number_bride = '010-9908-7299'

    let message;
    let show_message;

    function copyToClipboard(account_number) {
        navigator.clipboard.writeText(account_number).then(() => {
            message = '계좌번호가 복사되었습니다.';
            show_message = true;
        });
    }
</script>