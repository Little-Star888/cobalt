<script lang="ts">
    import { onMount } from "svelte";
    import { t } from "$lib/i18n/translations";
    import IconComet from "@tabler/icons-svelte/IconComet.svelte";

    let dismissed = true;

    onMount(() => {
        setTimeout(() => {
            dismissed = false;
        }, 200)
    });
</script>

<div id="update-notification" role="alert" aria-atomic="true">
    <button
        class="button update-button"
        class:visible={!dismissed}
        on:click={() => {
            dismissed = true;
            window.location.reload()
        }}
    >
        <div class="update-icon">
            <IconComet />
        </div>
        <div class="update-text">
            <div>{$t("notification.update.title")}</div>
            <div class="subtext">{$t("notification.update.subtext")}</div>
        </div>
    </button>
</div>

<style>
    #update-notification {
        position: absolute;
        display: flex;
        justify-content: end;
        align-items: center;
        width: 100%;
        pointer-events: none;
        z-index: 2;
    }

    .update-button {
        padding: 8px 12px 8px 8px;
        pointer-events: all;
        gap: 8px;
        margin: 0 64px;
        margin-top: calc(env(safe-area-inset-top) + 8px);
        box-shadow:
            var(--button-box-shadow),
            0 0 10px 0px var(--button-elevated-hover);
        border-radius: 14px;

        transform: translateY(-150px);
        transition: transform 0.4s cubic-bezier(0.53, 0.05, 0.23, 1.15);
    }

    .update-button.visible {
        transform: none;
    }

    .update-icon {
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: var(--button-elevated-hover);
        padding: 3px;
        border-radius: 6px;
    }

    .update-icon :global(svg) {
        stroke-width: 1.5px;
        width: 25px;
        height: 25px;
        will-change: transform;
    }

    .update-text {
        display: flex;
        flex-direction: column;
        text-align: start;
        font-size: 12.5px;
    }

    .subtext {
        padding: 0;
        user-select: none;
        -webkit-user-select: none;
    }

    .update-text,
    .subtext {
        line-height: 1.2;
    }

    @media screen and (max-width: 535px) {
        #update-notification {
            bottom: calc(var(--sidebar-height-mobile) + 16px);
            justify-content: center;
        }

        .update-button {
            transform: translateY(300px);
            margin: 0;
            transition: transform 0.55s cubic-bezier(0.53, 0.05, 0.23, 1.15);
        }
    }
</style>
