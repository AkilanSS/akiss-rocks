<script lang="ts">

    import { gsap } from "gsap";
    import { onMount } from "svelte";

    import { SplitText } from "gsap/dist/SplitText";
    import { TextPlugin } from "gsap/dist/TextPlugin";

    gsap.registerPlugin(SplitText,TextPlugin);
    
    let tl = gsap.timeline();

    onMount(() => {
        let split = SplitText.create("#name",{
            type: "chars",
            mask: "words"
        })

        tl.from(split.chars, {
            opacity: 0,
            x: 10,
            stagger: 0.1,
            duration: 0.5
        })

        tl.from("#bio-line", {
            delay: 0.5,
            opacity: 0,
            y: 10,
            duration: 0.5
        }, "<")

        tl.from(".l-logo", {
            opacity: 0
        }, "+=0")

        tl.from("#flower", {
            opacity: 0
        }, "<")

        tl.to("#flower",{
            rotation: 360,
            repeat: -1,
            duration: 5,
            ease: "expo"
        }, "<");
    }); 

</script>

<div id="main-ctn">
    <div id="header">
        <div id="name-ctn">
            <div id="name-sub-ctn">
                <span id="name">Akilan</span>
                <img id="flower" src="vectors/flower-big.svg" alt="">
            </div>
            <span id="bio-line">I do cool stuff, occasionally</span>
            <a class="l-logo" href="http://github.com/AkilanSS/" target="_blank"><img src="vectors/github.svg" alt=""></a>
            <a class="l-logo" id="linkedin-logo" href="http://linkedin.com/in/akilanss" target="_blank"><img src="/vectors/linkedin.svg" alt=""></a>
        </div>
        <div id="status-ctn">

        </div>
    </div>
    <div id="nav">
        <div id="akiss-logo">
            <img src="vectors/akiss-rocks-logo.svg" alt="" srcset="">
        </div>
        <div id="nav-menu-wrap">
            <div class="nav-menu-ctn" id="nav1"><span id="text-nav1">BLOG</span></div>
            <div class="nav-menu-ctn" id="nav2"><span id="text-nav1">PROJECTS</span></div>
            <div class="nav-menu-ctn" id="nav3"><span id="text-nav1">SANDBOX</span></div>
            <div class="nav-menu-ctn" id="nav4"><span id="text-nav1">ALGORITHMS</span></div>
        </div>
        <div style="margin-left: auto;"></div> <!--For pushing the logo to the rigght-->
        <div id="kessoku-logo">
            <img src="vectors/kessoku-band-logo.svg" alt="" srcset="">
        </div>
    </div>
    <div id="recent-project-ctn">
        <span class="ctn-head">Recent Projects</span>
        <div id="project-ctn-wrap">
            <div class="project-ctn" id="project-id-1">
                <span id="project-name">
                    STEADY STATE VISUALLY EVOKED POTENTIALS
                </span>
                <div id="project-info-ctn" style="display:none">

                </div>
            </div>
            <div class="project-ctn" id="project-id-2">
                <span id="project-name">
                    SHELLY - SSH OVER HTTPS
                </span>
                <div id="project-info-ctn" style="display:none">

                </div>
            </div>
            <div class="project-ctn" id="project-id-2">
                <span id="project-name">
                    HODGKIN-HUXLEY NEURONAL MODELLING
                </span>
                <div id="project-info-ctn" style="display:none">

                </div>
            </div>
            <div class="project-ctn" id="project-id-2">
                <span id="project-name">
                    GIVESYNC
                </span>
                <div id="project-info-ctn" style="display:none">

                </div>
            </div>
        </div>
    </div>
    <div id="recent-post-ctn" class="light-ctn">
        <span id="recent-post-head">Recent Posts</span>
        <div id="all-post-ctn">
            <div class="post-ctn" id="post-ctn-1">
                <div class="post-img">
                    <div class="date"></div>
                    <!--Image should go herre-->
                </div>
                <div class="post-title">Defining the Eigen Value Problem</div>
            </div>
            <div class="post-ctn" id="post-ctn-1">
                <div class="post-img">
                    <div class="date"></div>
                    <!--Image should go herre-->
                </div>
                <div class="post-title">Defining the Eigen Value Problem</div>
            </div>
            <div class="post-ctn" id="post-ctn-1">
                <div class="post-img">
                    <div class="date"></div>
                    <!--Image should go herre-->
                </div>
                <div class="post-title">Defining the Eigen Value Problem</div>
            </div>
            <div class="post-ctn" id="post-ctn-1">
                <div class="post-img">
                    <div class="date"></div>
                    <!--Image should go herre-->
                </div>
                <div class="post-title">Defining the Eigen Value Problem</div>
            </div>
        </div>
    </div>
    <div class="light-ctn" id="spotlight-ctn">
        <span id="light-head">Spotlight of the Moment</span>
        <div id="light-sub-ctn">
            <div id="light-txt-ctn">
                <span id="light-txt-head">
                    Non Linear Recurrent Networks for State Transition under Diffeomorphic Topological Space through Riemannian Lie Algebraic Rings
                </span>
                <span id="light-txt-desc">
                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi. In eros mauris, elementum nec auctor vel, imperdiet et mi. Morbi dignissim maximus nunc, eu lobortis justo pulvinar at.                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi. In eros mauris, elementum nec auctor vel, imperdiet et mi. Morbi dignissim maximus nunc, eu lobortis justo pulvinar at.
                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi. In eros mauris, elementum nec auctor vel, imperdiet et mi. Morbi dignissim maximus nunc, eu lobortis justo pulvinar at.
                </span>
            </div>
            <div id="img-ctn">

            </div>
        </div>
    </div>
    <!-- <div id="gallery-ctn" class="light-ctn">

    </div> -->
    <div id="footer">
        <div id="footer-wrap">
        <span id="kural-tamil-text">
            “இடுக்கண் வருங்கால் நகுக அதனை <br>
            அடுத்தூர்வது அஃதொப்ப தில்.”
        </span> 
        <span id="kural-eng-text">
            “Laugh at misfortune. There is nothing so able, To triumph over it.”
        </span>
        <span id="kural-num">
            திருக்குறள் - ௬௱௨௰௧
        </span>
        </div>
    </div>
</div>


