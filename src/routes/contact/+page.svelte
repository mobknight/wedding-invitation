<div class="block pt-5 pr-5 mr-5">
    <div class="columns is-mobile">
        <div class="column has-text-right">
            <span class="is-size-4">신랑</span>
        </div>
        <div class="column is-narrow">
            <a href="tel://{phone_number_groom}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiPhone} size=48></SvgIcon>
                </span>
            </a>
        </div>
        <div class="column is-narrow">
            <a href="sms://{phone_number_groom}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiMessageProcessing} size=48></SvgIcon>
                </span>
            </a>
        </div>
    </div>
</div>
<div class="block pr-5 mr-5">
    <div class="columns is-mobile">
        <div class="column has-text-right">
            <span class="is-size-4">신부</span>
        </div>
        <div class="column is-narrow">
            <a href="tel://{phone_number_bride}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiPhone} size=48></SvgIcon>
                </span>
            </a>
        </div>
        <div class="column is-narrow">
            <a href="sms://{phone_number_bride}">
                <span class="icon is-medium">
                    <SvgIcon type="mdi" path={mdiMessageProcessing} size=48></SvgIcon>
                </span>
            </a>
        </div>
    </div>
</div>


<div class="container p-5">
    <div class="content has-text-right is-large">
        마음 전하실 곳
    </div>
    <div class="columns is-mobile">
        <div class="column has-text-right">
            <span class="is-size-4">신랑</span>
        </div>
        <div class="column is-narrow">
            <button class="button" on:click={() => {copyToClipboard('토스뱅크 1000-0610-6759')}}>계좌번호 복사</button>
            <a class="button" href="https://link.kakaopay.com/_/fq5Dm59" target="_blank" style="background-color:#FAE100;">
                <figure class="image">
                    <img src={kakaopay} alt="" style="height:1.5rem; width:4rem;"/>
                </figure>
            </a>
        </div>
    </div>
    <div class="columns is-mobile">
        <div class="column has-text-right">
            <span class="is-size-4">신부</span>
        </div>
        <div class="column is-narrow">
            <button class="button" on:click={() => {copyToClipboard('토스뱅크 1000-0740-3010')}}>계좌번호 복사</button>
            <a class="button" href="https://link.kakaopay.com/_/yqJaIoR" target="_blank" style="background-color:#FAE100;">
                <figure class="image">
                    <img src={kakaopay} alt="" style="height:1.5rem; width:4rem;"/>
                </figure>
            </a>
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