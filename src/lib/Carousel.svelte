<script lang="ts">
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
            description: "Build websites with custom to-do lists, galleries of your projects, keep track of your favorite restaurants, and do anything else you might be able to imagine.",
            images: ["https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTVSX2ePH_Ni4g0vaM3td4po-87fE8yrdfSJA&s", "https://img.itch.zone/aW1hZ2UvMzg1NjIyMy8yMzAwNTQ3MC5wbmc=/original/fR9eCD.png"],
            captions: ["Example example 1", "Example example 2"]
        },
        {
            id: 'Websites',
            heading: "Web Development",
            description: "Build websites with custom to-do lists, galleries of your projects, keep track of your favorite restaurants, and do anything else you might be able to imagine.",
            images: ["https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTVSX2ePH_Ni4g0vaM3td4po-87fE8yrdfSJA&s", "https://img.itch.zone/aW1hZ2UvMzg1NjIyMy8yMzAwNTQ3MC5wbmc=/original/fR9eCD.png"],
            captions: ["Example example 1", "Example example 2"]
        },
        {
            id: 'Games',
            heading: "Game Development",
            description: "Build websites with custom to-do lists, galleries of your projects, keep track of your favorite restaurants, and do anything else you might be able to imagine.",
            images: ["https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTVSX2ePH_Ni4g0vaM3td4po-87fE8yrdfSJA&s", "https://img.itch.zone/aW1hZ2UvMzg1NjIyMy8yMzAwNTQ3MC5wbmc=/original/fR9eCD.png"],
            captions: ["Example example 1", "Example example 2"]
        }
    ]

    let selectedIndex = $state(1);
    let current = $derived(pathways[selectedIndex]);
</script>

<main class="container">
    <div class="this-is-just-a-wrapper-so-that-i-can-create-a-clip-path-shadow">
        <section class="project-bubble">
            <h2>{current.heading}</h2>
            <div class="list">
                <img src={current.images[0]} alt="" />
                <p>{current.captions[0]}</p>
                <img src={current.images[1]} alt="" />
                <p>{current.captions[1]}</p>
            </div>
        </section>
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

    .project-bubble {
        max-width: 30vw;
        background-color: #fcf8f2;
        padding: 2vw;
        clip-path: url(#responsiveClip);
    }

    .this-is-just-a-wrapper-so-that-i-can-create-a-clip-path-shadow {
        filter: drop-shadow(-3px 3px 1px rgba(0, 0, 0, 0.3));
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
        font-family: 'EG Garamond', serif;
        background-color: transparent !important;
    }

    .card h2 {
        font-style: normal;
        transition: opacity 0.3s ease-in-out, transform 0.3s ease-in-out;
        filter: opacity(0.6);
        transform: scale(0.5) translateY(-5vw);
    }

    .card.active h2 {
        filter: opacity(1);
        transform: scale(1);
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

</style>