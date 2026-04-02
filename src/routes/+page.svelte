<script lang="ts">

    import { gsap } from 'gsap';
    import { Draggable } from 'gsap/all';
    import InertiaPlugin from 'gsap/InertiaPlugin';
    import { SplitText } from 'gsap/SplitText';
    import { TextPlugin } from 'gsap/TextPlugin';
    import { ScrollTrigger } from 'gsap/ScrollTrigger';
    import { onMount } from 'svelte';
    import Lenis from 'lenis';
    import 'lenis/dist/lenis.css'; 

    let tl = gsap.timeline();

    let status_ctn: HTMLElement;
    let nav_ctn: HTMLElement;

    onMount(() => {
        const lenis = new Lenis({
            wheelMultiplier: 0.5,
            lerp: 0.2
        });

        

        function raf(time: number) {
            lenis.raf(time);
            requestAnimationFrame(raf);
        }
        requestAnimationFrame(raf);

        gsap.registerPlugin(SplitText,TextPlugin, ScrollTrigger, Draggable, InertiaPlugin);

        Draggable.create('#status-ctn', {
            type: 'x,y',
            bounds: "#main-ctn",
            trigger: "#status-flower",
            inertia: true,  
            onClick: function () {
                console.log('clicked');
            },
            onThrowComplete: () => {
                let curr_nav_ctn_pos = nav_ctn.getBoundingClientRect();
                let curr_status_ctn_pos = status_ctn.getBoundingClientRect();
                
                if (curr_status_ctn_pos.top > curr_nav_ctn_pos.top){
                    gsap.to(status_ctn, {
                        y: 0,
                        x: 0,
                        overwrite: true
                    })
                }
            }
        })

        console.log("PEAK1")

        gsap.to('#name-sub-ctn, #bio-line, #status-ctn', {
            display: 'flex',
            duration: 0.001,
        })

        console.log("PEAK2")
        let split = SplitText.create("#name",{
            type: "chars",
            mask: "words"
        })

        console.log("PEAK3")


        tl.from(split.chars, {
            opacity: 0,
            x: 10,
            stagger: 0.1,
            duration: 0.5,
        },'<')

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

        tl.from("#status-ctn", {
            opacity: 0,
            ease: "back"
        }, "<")

        tl.from("#status-flower", {
            rotate: 360,
            repeat: -1,
            duration: 10,
            ease: "none"
        })

        let ann_split = SplitText.create("#recent-ann", {
            type: "chars"
        })

        gsap.fromTo(ann_split.chars, {
                stagger: 0.2,
                y: 2,
                repeat: -1,
                yoyo: true,
                ease:  "power1.inOut"
            }, {
                stagger: 0.2,
                y: -2,
                repeat: -1,
                yoyo: true,
                ease:  "power1.inOut"
            }, 
        )
        lenis.on('scroll', ScrollTrigger.update);

        // gsap.to("#rest-wrap", {
        //     yPercent: -15,
        //     ease: "none",
        //     scrollTrigger : {
        //         trigger: "#header",
        //         start: "top top",
        //         end: 'bottom top',
        //         scrub: true
        //     }
        // })

        

        return () => {
            lenis.destroy();
        };
    });


    function handleHover(node: any){
        let text = node.children[0];
        let text_id = parseInt(node.id.slice(-1)) - 1;
        let split_char = SplitText.create(text, {
            type: "chars, words",
            mask: "lines"
        })

        let word_to_anim = split_char.words;
        let color = ["#E70047", "#87DADE", "#FDED74", "#016EBF"]
        let animation : gsap.core.Tween;
        animation = gsap.to(word_to_anim, {
                scale: 1.3,
                ease: "power4",
                paused: true
            })

        const onEnter = () => {
            console.log(animation)
            let char_to_change = split_char.chars[Math.floor(Math.random() * (split_char.chars.length))]
            gsap.to(char_to_change, {
                duration: 0.5,    
                color: color[text_id],
                rotation: 360
            })

            animation.play();
            
        }

        const onLeave = () => {
            console.log(animation)
            if (animation) {
                animation.reverse();
            }
        }

        node.addEventListener('mouseenter', onEnter);
        node.addEventListener('mouseleave', onLeave);
    }

    function animateHairpin(node: any){
        const hairpin_img = node.children[1];
        let animation : gsap.core.Tween;
        const onEnter = () => {
            animation = gsap.to(hairpin_img, {
                rotation: 360,
                ease: 'power4',
                duration: 1 
            })  
        }

        const onLeave = () => {
            if (animation) animation.reverse();
        }

        node.addEventListener('mouseenter', onEnter);
        node.addEventListener('mouseleave', onLeave);
    }

        function handleProjectCtn(node: any){
            let project_name_ctn = node.children[0];
            let project_info_ctn = node.children[1];

            let tl = gsap.timeline({paused: true})
            tl.set(project_info_ctn, {display: 'flex'})
            tl.to(project_info_ctn, {
                    duration: 0.3,
                    height: 'auto',
                    ease: 'power4.inOut'
                })
            tl.from(project_info_ctn, {
                opacity: 0,
                duration: 0.3
            },'<')
            node.addEventListener('mouseenter', () => {
                tl.play()
            })

            node.addEventListener('mouseleave', () => {
                tl.reverse();
            })
        }


    
</script>

<div id="main-ctn">
    <div id="header">
        <div id="name-ctn">
            <div id="name-sub-ctn">
                <span id="name">Akilan</span>
                <img id="flower" src="vectors/flower-big.svg" alt="">
            </div>
            <div id="name-desc-ctn">
                <span id="bio-line">I do cool stuff, occasionally</span>
                <div id="name-link-ctn">
                    <a class="l-logo" href="http://github.com/AkilanSS/" target="_blank"><img src="vectors/github.svg" alt=""></a>
                <a class="l-logo" id="linkedin-logo" href="http://linkedin.com/in/akilanss" target="_blank"><img src="/vectors/linkedin.svg" alt=""></a>
                </div>
            </div>
            
        </div>
        <div id="status-ctn" bind:this={status_ctn}>
            <img src="vectors/flower-small.svg" id="status-flower" role="presentation" alt="" srcset="">
            <span id="status-ctn-head">
                What's on Akilan's mind lately?
            </span>
            <div id="ann-ctn">
                <span class="ann">
                    <span class="ann-type type-blog"><span id="recent-ann">[NEW]</span>[BLOG]</span> 
                    <span class="ann-text">Is big chungus real?</span>
                </span>
                <span class="ann">
                    <span class="ann-type type-blog">[BLOG]</span>
                    <span class="ann-text">A guide on being pretty</span>
                </span>
                <span class="ann">
                    <span class="ann-type type-musings">[MUSINGS]</span>
                    <span class="ann-text">இனியவை கூறல்</span>
                </span>
            </div>
        </div>
    </div>
    <div id="rest-wrap">
        <div id="nav" bind:this={nav_ctn}>
        <div use:animateHairpin id="akiss-logo">
            <img id="akiss-logo-img" src="vectors/akiss-rocks-logo-without-hairpin.svg" alt="" srcset="">
            <img id="nav-hairpin-logo" src="vectors/hairpin.svg" alt="" srcset="">
        </div>
        <div id="nav-menu-wrap">
            <a href="" use:handleHover class="nav-menu-ctn" id="nav1"><span id="text-nav1">BLOG</span></a>
            <a href="" use:handleHover class="nav-menu-ctn" id="nav2"><span id="text-nav2">PROJECTS</span></a>
            <a href="" use:handleHover class="nav-menu-ctn" id="nav3"><span id="text-nav3">SANDBOX</span></a>
            <a href="" use:handleHover class="nav-menu-ctn" id="nav4"><span id="text-nav4">ALGORITHMS</span></a>
        </div>
        <!--For pushing the logo to the rigght-->
        
        <img id="kessoku-logo" src="vectors/kessoku-band-logo.svg" alt="" srcset="">
        
    </div>
    <div id="recent-project-ctn">
        <span class="ctn-head">Recent Projects</span>
        <div id="project-ctn-wrap">
            <div class="project-ctn" id="project-id-1" use:handleProjectCtn>
                <span class="project-name">
                    STEADY STATE VISUALLY EVOKED POTENTIALS
                </span>
                <div class="project-info-ctn">
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                </div>
            </div>
            <div class="project-ctn"  id="project-id-1" use:handleProjectCtn>
                <span class="project-name">
                    STEADY STATE VISUALLY EVOKED POTENTIALS
                </span>
                <div class="project-info-ctn">
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                </div>
            </div>
            <div class="project-ctn" id="project-id-1" use:handleProjectCtn>
                <span class="project-name">
                    STEADY STATE VISUALLY EVOKED POTENTIALS
                </span>
                <div class="project-info-ctn">
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                </div>
            </div>
            <div class="project-ctn" id="project-id-1" use:handleProjectCtn>
                <span class="project-name">
                    STEADY STATE VISUALLY EVOKED POTENTIALS
                </span>
                <div class="project-info-ctn">
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
                    <div class="info-ctn-sec">
                        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. In eu purus eget tortor venenatis tempus vitae et erat. Praesent dolor elit, dictum vel velit non, varius malesuada nisi.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec nec lacinia dui. Nullam tempor nibh mauris, egestas mollis augue hendrerit in. 
                    </div>
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
</div>


