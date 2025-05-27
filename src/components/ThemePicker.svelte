<script lang="ts">
    import { argbFromHex, themeFromSourceColor, applyTheme } from "@material/material-color-utilities";
    import { getMissingColorMap } from "../lib/materialColorUtilitiesExtend";
    import Tokens from "../types/Tokens";

    let themeColor = $state('#86468C')
    let debugElements = $state(false)
    let baseColor = $state('--md-sys-color-surface')

    let hoverStateLayerOpacity = $state('0.08')
    let activeStateLayerOpacity = $state('0.1')

    $effect(() => {
        const systemDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
        const theme = themeFromSourceColor(
            argbFromHex(themeColor)
        )
		applyTheme(
            theme, {
                target: document.documentElement,
                dark: systemDark
            }
        );
        for (const [key, value] of getMissingColorMap(theme, systemDark)) {
            document.documentElement.style.setProperty(key, value);
        }
        document.documentElement.style.setProperty('--base-color', `var(${baseColor})`)
        document.documentElement.style.setProperty('--debug-element-color', debugElements ? '#FF0000' : '')
        document.documentElement.style.setProperty('--md-sys-state-hover-state-layer-opacity', hoverStateLayerOpacity)
        document.documentElement.style.setProperty('--md-sys-state-active-state-layer-opacity', activeStateLayerOpacity)
    });
</script>

<div class="container">
    <h2>Theme controls</h2>
    <label id="hex" class="input-group" for="color-input">
        <span class="label">Hex Source Color</span>
        <span class="input-wrapper">
            <div class="overflow">
                <input id="color-input" type="color" bind:value={themeColor}>
            </div>
        </span>
    </label>

    <label id="base" class="input-group" for="base-color">
        <span class="label">Base Color</span>
        <select name="base-color" id="base-color" bind:value={baseColor}>
            {#each Tokens as token}
                <option value={token}>{token}</option>
            {/each}
        </select>
    </label>

    <hr />

    <label id="hoverOpacity" class="input-group" for="hover-state-layer-opacity">
        <span class="label">Hover State Layer Opacity</span>
        <input type="number" min="0" max="1" step="0.005" name="hoverOpacity" id="hover-state-layer-opacity" bind:value={hoverStateLayerOpacity} />
    </label>

    <label id="activeOpacity" class="input-group" for="active-state-layer-opacity">
        <span class="label">Active State Layer Opacity</span>
        <input type="number" min="0" max="1" step="0.005" name="activeOpacity" id="active-state-layer-opacity" bind:value={activeStateLayerOpacity} />
    </label>

    <hr />

    <label id="debug" class="input-group" for="debug-elements">
        <span class="label">Debug Elements Visible</span>
        <span class="input-wrapper">
            <div class="overflow">
                <input id="debug-elements" type="checkbox" bind:checked={debugElements}>
            </div>
        </span>
    </label>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        gap: 12px;
    }

    h2 {
        margin: 0 4px;
    }

    hr {
        width: 100%;
        background-color: var(--md-sys-color-outline-variant);
        border-color: var(--md-sys-color-outline-variant);
        margin-block: -2px;
    }

    label {
        padding-inline: 12px;
        border-radius: 12px;
        background-color: var(--md-sys-color-surface-variant);
        color: var(--md-sys-color-on-surface-variant);
        --md-slider-inactive-track-color: var(--md-sys-color-on-surface-variant);
    }
    #hex {
        background-color: var(--md-sys-color-primary-container);
    }
    .input-group {
        display: flex;
        padding: 8px 12px;
        align-items: center;
    }
    .input-group .label {
        flex-grow: 1;
    }
    .input-group .input-wrapper {
        box-sizing: border-box;
        overflow-x: auto;
        width: 40px;
        height: 40px;
        box-sizing: border-box;
        border: 1px solid var(--md-sys-color-on-secondary-container);
        position: relative;

        border-radius: 50%;

        display: flex;
        align-items: center;
        justify-content: flex-end;
    }
    .overflow {
        width: 100%;
        height: 100%;
        overflow: hidden;
        border-radius: inherit;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .input-group input[type='color'] {
        min-width: 200%;
        min-height: 200%;
    }
    .input-group input[type='checkbox'] {
        min-width: 110%;
        min-height: 110%;
    }
    .input-group select, .input-group input[type='number'] {
        font: inherit;

        background-color: var(--md-sys-color-surface-container-low);
        border: 1px solid var(--md-sys-color-outline);
        border-radius: 12px;
        padding: 0 8px;
        height: 40px;
        font-family: monospace;

        max-width: 200px;

        &:focus {
            outline: 3px solid var(--md-sys-color-primary);
            outline-offset: -3px;
        }
    }
</style>