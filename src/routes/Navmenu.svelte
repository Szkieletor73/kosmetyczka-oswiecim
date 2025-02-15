<script lang="ts">
	import { assets } from "$app/paths";
	import { page } from "$app/state";
    import "iconify-icon";

    let mobileMenuExpanded = $state(false);
</script>

{#snippet navlink(name: string, href: string)}
    <li>
        <a href="{href}" class="navlink">
            <button class="navlink-button" class:active="{page.url.pathname.includes(href)}">
                {name}
            </button>
        </a>
    </li>
{/snippet}

<nav class="container" class:expanded={mobileMenuExpanded}>
    <div class="mobile-toggle">
        <input type="checkbox" id="mobile-toggle-check" aria-label="Toggle navigation menu" bind:checked={mobileMenuExpanded} />
        <span></span>
        <span></span>
        <span></span>
    </div>

    <a class="logo" href="/">
        <img src="{assets}/logo-text.svg" class="logo-title" alt="Madame Diana logo" />
        <div>
            <!-- Placeholder for logo emblem -->
        </div>
        <div class="logo-subtitle">
            Salon Kosmetyczny
        </div>
    </a>

    <div class="contact-blurb">
        <div>
            <strong>Oświęcim</strong>
        </div>
        <div>
            <iconify-icon inline icon="mdi:map-marker"></iconify-icon> ul. 3 Maja 8D
        </div>
        <div>
            <iconify-icon inline icon="mdi:phone"></iconify-icon> tel. 504 061 279
        </div>
    </div>

    <ul class="links">
        {@render navlink("Oferta", "/oferta")}
        {@render navlink("Cennik", "/cennik")}
        {@render navlink("Pomysł na prezent", "/karty-upominkowe")}
        {@render navlink("Kontakt", "/kontakt")}
        {@render navlink("O nas", "/about")}
    </ul>
</nav>

<style>
    .container {
        width: 100%;
        position: sticky;

        min-height: var(--nav-height);
        padding: 8px var(--page-margin);

        background: transparent;
        color: var(--color-on-background);
        border-bottom: 1px solid var(--color-on-background);

        display: grid;
        grid-template:
            "logo links contact" 1fr
            "logo links contact" auto / auto 1fr auto;
        column-gap: 32px;
        row-gap: 24px;
    }

    .mobile-toggle {
        display: none;
    }

    .mobile-toggle {
        display: initial;
        position: absolute;
        top: 0;
        left: 0;
        padding: 0;

        background: transparent;
        border: none;

        cursor: pointer;

        width: 92px;
        height: 92px;
    }

    .mobile-toggle #mobile-toggle-check {
        width: 100%;
        height: 100%;
        position: absolute;
        opacity: 0;
    }
    
    .logo {
        grid-area: logo;

        align-self: center;
        display: grid;
        grid-template:
            "title emblem" 1fr
            "subtitle emblem" auto / 1fr auto;
    }

    .logo-title {
        height: 82px;
    }

    .logo-subtitle {
        font-family: "Montserrat";
        font-weight: 600;
        text-align: center;
        color: var(--color-on-background);
    }

    .links {
        grid-area: links;

        height: fit-content;

        align-self: end;
        list-style: none;
        display: flex;
        flex-wrap: wrap;
        gap: 12px;
        margin: 0;
    }

    .navlink-button {
        font-size: 18px;
        font-family: "Montserrat";

        cursor: pointer;

        border: none;
        border-bottom: 2px solid transparent;

        background: transparent;
        color: var(--color-on-background);

        padding: 8px 16px;

        transition-property: color, background-color, border-bottom-color;
        transition-duration: 0.2s;
    }

    .navlink-button:hover {
        color: var(--color-primary);
        background-color: #ffffffcc;
        border-bottom-color: var(--color-primary);
    }

    .navlink-button.active {
        color: var(--color-primary);
        border-bottom-width: 4px;
        border-bottom-color: var(--color-primary);
        padding: 8px 16px 6px 16px;
    }

    .contact-blurb {
        grid-area: contact;
        height: fit-content;
        align-self: end;

        margin: 8px 16px;

        display: flex;
        flex-wrap: wrap;
        gap: 16px;
    }

    .contact-blurb div {
        cursor: text;
    }

    /* Mobile styles */
    @media only screen and (max-width: 1280px) {
        .container {
            display: flex;
            flex-direction: column;
            max-height: 100vh;
            padding: 8px var(--page-margin-mobile);
            min-height: initial;
            height: 92px;
            overflow: hidden;
        }

        .container.expanded {
            height: initial;
        }

        .mobile-toggle span {
            width: 50%;
            border-top: 4px solid var(--color-on-background);
            position: absolute;
            left: 0;
            right: 0;
            margin: auto;
            pointer-events: none;
            transition-property: top, transform, width;
            transition-duration: 0.4s;
            transition-timing-function: cubic-bezier(0.6, -0.28, 0.735, 0.045);
        }
        .mobile-toggle span:nth-of-type(1) {
            top: 37%;
        }
        .mobile-toggle span:nth-of-type(2) {
            top: 50%;
        }
        .mobile-toggle span:nth-of-type(3) {
            top: 63%;
        }

        #mobile-toggle-check:checked ~ span:nth-of-type(1) {
            top: 50%;
            transform: rotateZ(45deg);
        }
        #mobile-toggle-check:checked ~ span:nth-of-type(2) {
            width: 1px;
        }
        #mobile-toggle-check:checked ~ span:nth-of-type(3) {
            top: 50%;
            transform: rotateZ(-45deg);
        }

        .logo-title {
            height: 48px;
        }

        .links {
            width: 100%;
            align-self: center;
            flex-direction: column;
            flex-wrap: nowrap;
            overflow-y: auto;
        }

        .navlink-button {
            width: 100%;
            /* text-align: left; */
            border-bottom: none;
            border-left: 2px solid transparent;
            transition-property: color, background-color, border-left-color;
        }

        .navlink-button:hover {
            border-left-color: var(--color-primary);
        }

        .navlink-button.active {
            border-left-color: var(--color-primary);
            border-left-width: 4px;
        }

        .contact-blurb {
            align-self: center;
        }
    }
</style>