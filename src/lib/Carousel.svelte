<script lang="ts">
    import { fade, fly } from 'svelte/transition';

    interface Pathway {
        id: 'Websites' | 'Apps' | 'Games';
        heading: string;
        description: string;
        images: string[];
        captions: string[];
    }

    const pathways: Pathway[] = [
        {
            id: 'Apps',
            heading: "App Development",
            description: "Build mobile and desktop apps that you can actually deploy on a store.",
            images: ["/images/pathways/logic-lab.png", "/images/pathways/kapong.png"],
            captions: ["Logic Lab, an educational platform for learning logical fallacies.", "Kapong, a pong remix."]
        },
        {
            id: 'Websites',
            heading: "Web Development",
            description: "Build websites with custom to-do lists, galleries of your projects, keep track of your favorite restaurants, and do anything else you might be able to imagine.",
            images: ["/images/pathways/prototype.png", "/images/pathways/projects-spa.png"],
            captions: ["Prototype, a website to recap an awesome event.", "A projects portfolio to send to employers."]
        },
        {
            id: 'Games',
            heading: "Game Development",
            description: "Build video games that are addictive, silly, moving, or just plainly fun.",
            images: ["/images/pathways/hachiware-game.png", "/images/pathways/crunch-time.png"],
            captions: ["Hachiware game, a dino game remake with new beloved characters.", "Crunch Time, a gacha game where aliens gather energy drinks."]
        }
    ]

    let selectedIndex = $state(1);
    let current = $derived(pathways[selectedIndex]);
</script>

<main class="container">
    <div class="this-is-just-a-wrapper-so-that-i-can-create-a-clip-path-shadow">
        {#key selectedIndex}
            <section class="project-bubble" in:fly={{ x: -20, duration: 400, delay: 200 }} out:fade={{ duration: 200 }}>
                <h2><b>{current.heading}</b></h2>
                <p>{current.description}</p>
                <div class="list">
                    <img src={current.images[0]} alt="" />
                    <p><i>{current.captions[0]}</i></p>
                    <img src={current.images[1]} alt="" />
                    <p><i>{current.captions[1]}</i></p>
                </div>
            </section>
        {/key}
    </div>
    <div>
        <div>
            <h1>Don't know where to start?</h1>
            <h1><b><i>We'll teach you.</i></b></h1>
            <section class="carousel">
                <button class="nav" onclick={() => (selectedIndex = (selectedIndex - 1 + pathways.length) % pathways.length)}>←</button>
                {#each pathways as path, i}
                    <button class="card" class:active={selectedIndex === i} onclick={() => (selectedIndex = i)}>
                        <img src="/images/gargoyle-sitting.png" alt="sitting gargoyle" />
                        <h2>{path.id}</h2>
                    </button>
                {/each}
                <button class="nav" onclick={() => (selectedIndex = (selectedIndex + 1) % pathways.length)}>→</button>
            </section>
        </div>
    </div>
</main>
<svg style="width:0;height:0;position:absolute;" aria-hidden="true"><clipPath id="responsiveClip" clipPathUnits="objectBoundingBox"><path d="M.99.11L.94 0 0 .01l.01.07L0 .28l.02.14L.01.42l.01.19.01.31L0 1l.97-.01 1-.04-.02-.21 1-.24-.03-.24.02-.15z"/></clipPath></svg>

<style>
    h1 {
        font-style: normal;
        font-weight: normal;
        text-align: center;
        margin: 0;
        line-height: 1;
    }

    h2 {
        margin: 0;
        font-style: italic;
        font-weight: normal;
    }

    .container {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 5vw 5vh;
        justify-content: space-between;
        gap: 2vw;
    }

    .this-is-just-a-wrapper-so-that-i-can-create-a-clip-path-shadow {
        filter: drop-shadow(-3px 3px 0 color-mix(in srgb, var(--dark-brown), transparent 60%));
        display: grid;
        place-items: center;
    }

    .project-bubble {
        max-width: 30vw;
        background-color: #fcf8f2;
        padding: 2vw;
        clip-path: url(#responsiveClip);
        grid-area: 1/1;
        transform: rotate(1deg);
    }

    .project-bubble img {
        object-fit: contain;
        width: 100%;
    }

    .project-bubble p {
        margin: 0;
    }

    .card.active {
        font-weight: bold;
    }

    .nav {
        /* color: white; */
        font-weight: bolder;
    }

    .carousel {
        display: flex;
        align-items: center;
        gap: -2.5vw;
        margin-top: 3vw;
    }

    .carousel button {
        border: none;
        border-radius: 0.75rem;
        padding: 0.5rem;
        background-color: #fcf8f2;
        transition: filter 0.1s ease-in-out;
    }

    .card {
        display: flex;
        flex-direction: column;
        font-family: 'EB Garamond', serif;
        background-color: transparent !important;
    }

    .card h2 {
        font-style: normal;
        transition: opacity 0.3s ease-in-out, transform 0.3s ease-in-out;
        filter: opacity(0.6);
        transform: scale(0.8) translateY(-4vw);
    }

    .card.active h2 {
        filter: opacity(1);
        transform: scale(1);
        font-weight: bold;
    }

    .card img {
        max-width: 20vw;
        transition: filter 0.3s ease-in-out, transform 0.3s ease-in-out;
        filter: opacity(0.6);
        transform: scale(0.5);
    }

    .card.active img {
        filter: opacity(1);
        transform: scale(1);
    }


    .carousel button:hover {
        filter: brightness(0.95);
    }

    .carousel button:active {
        filter: brightness(0.9);
    }

    @media (max-width: 768px) {
        .project-bubble {
            max-width: 100vw;
            position: static;
        }
        .container {
            flex-direction: column-reverse;
            margin-top: 10vw;
            margin-bottom: 5vw;
        }
    }

</style>