<script lang="ts">
	import { onMount } from "svelte";

    export let dialog: HTMLElement;
    onMount( () => {
        dialog.addEventListener('wheel', (e) => {
            e.stopPropagation();
        });
        dialog.addEventListener('touchmove', (e) => {
            e.stopPropagation();
        })
    })
    
</script>

<style>
    dialog{
        max-height: 60dvh;
        inline-size: 60vw;
        padding: clamp(2rem, 8vw, 5rem) clamp(1rem, 8vw, 10rem);
        font-family: 'Cooper Hewitt';
        background-color: #FEFEEB;
        overflow: hidden;
        border: 6px solid #FE6596;
        border-radius: 24px;
    }

    dialog::backdrop{
        background-color: #ffbad086;
    }

    dialog::before{
        content: "";
        position: absolute;
        bottom: 0;
        left: 0;
        height: 30%;
        width: 100%;
        background: #FEFEEB;
        background: linear-gradient(0deg,rgba(254, 254, 235, 1) 0%, rgba(247, 247, 247, 0) 100%);
        z-index: 2 ;
        pointer-events: none;
    }

    #overlay-wrap-ctn{
        display: flex;
        flex-direction: column;
        gap: 30px;
        max-height: 60dvh;

        overflow: scroll;
        scrollbar-width: none;

        #changelog-ctn{
            display: flex;
            flex-direction: column;
            gap: 10px;

            #changelog-head{
                font-weight: 800;
                font-size: clamp(1.5rem, 2vw, 3rem);
                color: #FE6596;
            }

            #changelog-text{
                color: #E890AB;
                font-size: clamp(1rem, 1.5vw, 1.2rem);
                font-weight: 500
            }

            a{
                text-decoration: none;
                color: #E890AB;
                font-weight: 800;
            }
        }

        .log-ctn{
            display: flex;
            flex-direction: column;
            gap: 10px;
            .log-date{
                font-weight: 800;
                font-size: clamp(1rem, 1.5vw, 1.125rem);
                color: #FE6596;
            }

            .log-text{
                font-weight: 400;
                font-size: clamp(0.9rem, 1.2vw, 1.1rem);
                color: #3F0114;
            }
        }
    }

</style>

<dialog bind:this={dialog} closedby=any>
    <div id="overlay-wrap-ctn">
        <div id="changelog-ctn">
            <span id="changelog-head">Changelogs</span>
            <span id="changelog-text">Here I update what I've been doing recently. Think of this as a relevant and dynamic alternative to the 'About Me' pages you see - adopted from <a href="https://nownownow.com/" target="_blank">https://nownownow.com/</a></span>
        </div>
        <div class="log-ctn">
            <span class="log-date">Apr 14, 2026</span>
            <span class="log-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ante mi, malesuada vitae suscipit quis, efficitur non ligula. Nam interdum magna sit amet venenatis efficitur. Nulla vel congue dui. Aliquam luctus, velit ut ornare dapibus, magna mi tempus dolor, a aliquet risus enim dapibus eros. Nunc quis volutpat mi. Pellentesque tincidunt sit amet dolor vel auctor. Vivamus id fermentum sapien. Sed commodo et enim sit amet feugiat. Sed faucibus est eget molestie vestibulum. Nam vestibulum purus quam.</span>
        </div>
        <div class="log-ctn">
            <span class="log-date">Apr 14, 2026</span>
            <span class="log-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ante mi, malesuada vitae suscipit quis, efficitur non ligula. Nam interdum magna sit amet venenatis efficitur. Nulla vel congue dui. Aliquam luctus, velit ut ornare dapibus, magna mi tempus dolor, a aliquet risus enim dapibus eros. Nunc quis volutpat mi. Pellentesque tincidunt sit amet dolor vel auctor. Vivamus id fermentum sapien. Sed commodo et enim sit amet feugiat. Sed faucibus est eget molestie vestibulum. Nam vestibulum purus quam.</span>
        </div>
        <div class="log-ctn">
            <span class="log-date">Apr 14, 2026</span>
            <span class="log-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ante mi, malesuada vitae suscipit quis, efficitur non ligula. Nam interdum magna sit amet venenatis efficitur. Nulla vel congue dui. Aliquam luctus, velit ut ornare dapibus, magna mi tempus dolor, a aliquet risus enim dapibus eros. Nunc quis volutpat mi. Pellentesque tincidunt sit amet dolor vel auctor. Vivamus id fermentum sapien. Sed commodo et enim sit amet feugiat. Sed faucibus est eget molestie vestibulum. Nam vestibulum purus quam.</span>
        </div>
        <div class="log-ctn">
            <span class="log-date">Apr 14, 2026</span>
            <span class="log-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ante mi, malesuada vitae suscipit quis, efficitur non ligula. Nam interdum magna sit amet venenatis efficitur. Nulla vel congue dui. Aliquam luctus, velit ut ornare dapibus, magna mi tempus dolor, a aliquet risus enim dapibus eros. Nunc quis volutpat mi. Pellentesque tincidunt sit amet dolor vel auctor. Vivamus id fermentum sapien. Sed commodo et enim sit amet feugiat. Sed faucibus est eget molestie vestibulum. Nam vestibulum purus quam.</span>
        </div>
        <div class="log-ctn">
            <span class="log-date">Apr 14, 2026</span>
            <span class="log-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ante mi, malesuada vitae suscipit quis, efficitur non ligula. Nam interdum magna sit amet venenatis efficitur. Nulla vel congue dui. Aliquam luctus, velit ut ornare dapibus, magna mi tempus dolor, a aliquet risus enim dapibus eros. Nunc quis volutpat mi. Pellentesque tincidunt sit amet dolor vel auctor. Vivamus id fermentum sapien. Sed commodo et enim sit amet feugiat. Sed faucibus est eget molestie vestibulum. Nam vestibulum purus quam.</span>
        </div>
    </div>
</dialog>