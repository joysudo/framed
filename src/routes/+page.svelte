<script lang="ts">
    let activeFruit = $state("");
    const fruits = [
        { id: 'Squash', label: 'this is a squash', x: '10%', y: '10%', side: 'right', src: '/images/Squash.png', path: 'M1295 313L1303 322V300L1286 214.5L1241 175.5V151L1225 126L1192.5 130.5L1199 143H1216.5L1210.5 165.5L1165 162L1099.5 187.5L1020 250.5L1005.5 309L975 366L1037.5 381L1125 356L1196 366L1238 316.5L1295 313Z'},
        { id: 'Corn', label: 'corny ahh', x: '10%', y: '10%', side: 'right', src: '/images/Corn.png', path: 'M1038.5 382L1065 388.5L1110.5 454.5V539L1078.5 605L1176.5 545.5L1183.5 513L1218.5 501L1249 513L1287.5 492.5L1274 477.5L1287.5 435.5H1332.5L1374.5 455.5L1473.5 421.5L1529 367L1577 351L1524 341L1488 381L1473.5 368.5H1431L1382 354L1321 348.5L1293 314.5L1239 319L1195.5 368.5L1123 359.5L1038.5 382Z'},
        { id: 'Green Grapes', label: 'green green dress', x: '10%', y: '10%', side: 'left', src: '/images/Green Grapes.png', path: 'M845.5 421L935.5 367.5V310.5L907.5 200.5H852L835.5 250.5L816.5 246L791.5 208L735.5 214L725.5 183.5H667H625L575.5 232L563.5 261L581 295.5V321.5L558 345V385.5L593.5 396V418.5L492 513.5L481 539L454.5 552L447 585L471 604L481 636.5L465.5 641L454.5 664L460 684.5L558 646L606.5 657.5L633 691.5L668.5 673L672.5 652.5L715.5 616.5L706.5 592.5L735.5 589.5L758 604L816.5 564.5L809 513.5L845.5 421Z'},
        { id: 'Peaches', label: 'arizona iced tea', x: '10%', y: '10%', side: 'left', src: '/images/Peaches.png', path: 'M1107.5 539L1075.5 605L1107.5 616L1149 659.5L1168.5 735L1149 810.5L1086.5 845.5L1035 876L968 860L900.5 802L862 826.5H802.5L730 810.5L707.5 771.5L661 735L680.5 648L719 616L823.5 582.5L812 513L852 421.5L943.5 368.5L968 391L982 368.5L1062.5 391L1107.5 455.5V539Z'},
        { id: 'Purple Grapes', label: 'suni, whats ur favorite color', x: '10%', y: '10%', side: 'right', src: '/images/Purple Grapes.png', path: 'M1511.5 639L1514.5 678L1495.5 703L1463.5 717L1430 698L1402 714L1394.5 754.5L1364 741.5L1330 764.5V793.5L1364 802.5L1410 767.5L1402 785.5V819L1433.5 823L1463.5 805.5L1490 827L1519 819L1531 793.5L1591.5 819H1637L1658.5 775.5L1623.5 736.5L1633.5 714L1623.5 671.5L1577 635L1546.5 619L1511.5 639Z'},
        { id: 'Red Grapes', label: 'reddy or not', x: '10%', y: '10%', side: 'right', src: '/images/Red Grapes.png', path: 'M1330.5 440L1364.5 455V486L1388 493.5L1415 486L1474 519.5L1477 564L1437.5 582L1430.5 663.5H1454.5L1477 689L1462 713L1430.5 694L1399.5 713L1394 750.5L1364.5 738L1330.5 758L1307.5 791.5L1197 770L1156 791.5L1171.5 731L1151.5 657L1121 625.5L1131.5 578.5L1179.5 548.5L1186 517.5L1219 504.5L1250 517.5L1294 493.5L1278.5 474.5L1290.5 440H1330.5Z'},
        { id: 'Small Pear', label: 'the perfect pear', x: '10%', y: '10%', side: 'left', src: '/images/Small Pear.png', path: 'M291.5 634.5L289 614L280 636.5L236.5 673L216 723L236.5 784.5L289 816L355.5 798L389.5 738.5L381 702L345.5 655.5L291.5 634.5Z'},
        { id: 'Big Pear', label: 'mmm', x: '10%', y: '10%', side: 'left', src: '/images/Big Pear.png', path: 'M602 736H639L635 696L602 660L556.5 649.5L461 688.5L424.5 736L417 805.5L485 853L564.5 861.5L567 784.5L602 736Z'},
        { id: 'Rambutan', label: 'i dont think this is actually a rambutan but thats the only spiky fruit i know', x: '10%', y: '10%', side: 'left', src: '/images/Rambutan.png', path: 'M708.5 775.5L732 832L696.5 877.5L631 892.5L568.5 864V785.5L602.5 739.5H658.5L708.5 775.5Z'},
    ]
</script>

<section class="hero">
    {#each fruits as fruit}
        <img id="layer-{fruit.id}" class="fruit-layer" class:hovered={activeFruit === fruit.id} src={fruit.src} alt={fruit.id}>
    {/each}
    <svg class="hitbox-svg" viewBox="0 0 1920 1080" xmlns="http://www.w3.org/2000/svg">
        {#each fruits as fruit}
            <path d={fruit.path} class="hitbox" onmouseenter={() => activeFruit = fruit.id} onmouseleave={() => activeFruit = ""} role="presentation" />
        {/each}
    </svg>
    {#each fruits as fruit}
        <div class="fruit-label label-{fruit.side}" class:visible={activeFruit === fruit.id} style="top: {fruit.y}; {fruit.side === 'left' ? `left: 0; width: ${fruit.x};` : `left: ${fruit.x}; width: calc(100% - ${fruit.x});`}">
            {#if fruit.side === 'right'}
                <span class="label-dot"></span>
                <span class="label-line"></span>
                <span class="label-text"> {fruit.label}</span>
            {:else}
                <span class="label-text">{fruit.label} </span>
                <span class="label-line"></span>
                <span class="label-dot"></span>
            {/if}
        </div>
    {/each}
</section>

<style>
    .hero {
        width: min(100vw, 177.78vh);
        height: min(56.25vw, 100vh);
        display: flex;
        align-items: center
    }

    .fruit-layer {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: auto;
        object-fit: contain;
        pointer-events: none;
        transition: transform 0.3s ease, filter 0.3s ease;
    }

    .fruit-layer.hovered {
        transform: translate(-5px, -5px);
        filter: brightness(1.3) drop-shadow(5px 5px 0 rgba(0, 0, 0, 0.3));
    }

    .hitbox-svg {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: auto;
        fill: transparent;
    }

    .fruit-label {
        position: absolute;
        display: flex;
        align-items: center;
        opacity: 0;
        z-index: 100;
        transition: opacity 0.3s ease, transform 0.3s ease;
    }

    .fruit-label.visible {
        opacity: 1;
        transform: translateY(-50%) scale(1);
    }

    .label-left {
        padding-left: 5vw;
    }

    .label-right {
        padding-right: 5vw;
        box-sizing: border-box;
    }

    .label-line {
        flex-grow: 1;
        height: 1px;
        background-color: whitesmoke;
    }

    .label-dot {
        width: 6px;
        height: 6px;
        border-radius: 50%;
        background-color: whitesmoke;
    }
</style>