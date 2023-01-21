<script lang='ts'>
    import { onMount } from 'svelte'
    let navMobile = null;
    function handleClick(e) {
        const { classList } = navMobile;

        if (classList.contains('nav-mobile-active')) {
            classList.remove('nav-mobile-active')
            classList.add('nav-mobile-hidden')
        }
        else {
            classList.add('nav-mobile-active')
            classList.remove('nav-mobile-hidden')
        }
    }

    onMount(() => {
        navMobile = document.getElementById('nav-mobile');
    })


</script>

<header id="main-header" data-height-onload="84" data-height-loaded="true" data-fixed-height-onload="84" style="top: 0px;">
    <div class="container clearfix et_menu_container">
        <div class="logo_container">
            <a class='logo_anchor' href="https://css.seas.upenn.edu/">
                <img class='logo_img' src="https://css.seas.upenn.edu/wp-content/uploads/2021/09/WEBSITE-LOGO.png" alt="Computational Social Science Lab" id="logo" />
            </a>
        </div>
        <div id="et-top-navigation">
            <nav id="top-menu-nav">
                <ul id="top-menu" class="nav">
                    <li class="menu-item menu-item-type-custom menu-item-object-custom menu-item-has-children menu-item-2731">
                        <a class="menu-item-anchor" href='https://css.seas.upenn.edu/about/'>About</a>
                        <ul class="sub-menu">
                            <li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-1554">
                                <a class="sub-menu-item-anchor" href="https://css.seas.upenn.edu/about/lab/">The Lab</a>
                            </li>
                            <li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-2232">
                                <a class="sub-menu-item-anchor" href="https://css.seas.upenn.edu/about/community/">CSS Community</a>
                            </li>
                        </ul>
                    </li>
                    <li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-1747">
                        <a class="menu-item-anchor" href="https://css.seas.upenn.edu/people/">People</a>
                    </li>
                    <li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-has-children menu-item-37">
                        <a class="menu-item-anchor" href="https://css.seas.upenn.edu/research/">Research</a>
                        <ul class="sub-menu">
                            <li class="menu-item menu-item-type-custom menu-item-object-custom menu-item-735">
                                <a class="sub-menu-item-anchor" href="https://css.seas.upenn.edu/project/penn-map/">PennMAP</a>
                            </li>
                            <li class="menu-item menu-item-type-custom menu-item-object-custom menu-item-292">
                                <a class="sub-menu-item-anchor" href="https://css.seas.upenn.edu/project/virtual-lab/">Group Dynamics</a>
                            </li>
                            <li class="menu-item menu-item-type-custom menu-item-object-custom menu-item-291">
                                <a class="sub-menu-item-anchor" href="https://css.seas.upenn.edu/project/covid-philadelphia/">COVID-Philadelphia</a>
                            </li>
                            <li class="menu-item menu-item-type-custom menu-item-object-custom menu-item-377">
                                <a class="sub-menu-item-anchor" href="https://css.seas.upenn.edu/project/common-sense/">Common Sense</a>
                            </li>
                        </ul>
                    </li>
                    <li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-344">
                        <a class="menu-item-anchor" href="https://css.seas.upenn.edu/partnerships/">Partners</a>
                    </li>
                    <li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-58">
                        <a class="menu-item-anchor" href="https://css.seas.upenn.edu/publications/">Publications</a>
                    </li>
                    <li class="menu-item menu-item-type-post_type menu-item-object-page menu-item-105">
                        <a class="menu-item-anchor" href="https://css.seas.upenn.edu/blog-news-events/">News</a>
                    </li>
                </ul>
            </nav>
        </div>

        <div id="et-top-navigation-mobile">
            <nav id='top-menu-nav-mobile'>
                <div class='icon' on:click={handleClick}>
                    <div class='line'></div>
                    <div class='line'></div>
                    <div class='line'></div>
                </div>
                <ul id='nav-mobile' class="nav-mobile nav-mobile-hidden">
                    <li>
                        <a class="item-mobile" href='https://css.seas.upenn.edu/about/'>About</a>
                        <ul class="sub-menu-mobile">
                            <li class="sub-menu-list-mobile">
                                <a class="sub-item-mobile" href="https://css.seas.upenn.edu/about/lab/">The Lab</a>
                            </li>
                            <li class="sub-menu-list-mobile">
                                <a class="sub-item-mobile" href="https://css.seas.upenn.edu/about/community/">CSS Community</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a class="item-mobile" href='https://css.seas.upenn.edu/people/'>People</a>
                    </li>
                    <li>
                        <a class="item-mobile" href='https://css.seas.upenn.edu/research/'>Research</a>
                        <ul class="sub-menu-mobile">
                            <li class="sub-menu-list-mobile">
                                <a class="sub-item-mobile" href="https://css.seas.upenn.edu/project/penn-map/">PennMAP</a>
                            </li>
                            <li class="sub-menu-list-mobile">
                                <a class="sub-item-mobile" href="https://css.seas.upenn.edu/project/virtual-lab/">Group Dynamics</a>
                            </li>
                            <li class="sub-menu-list-mobile">
                                <a class="sub-item-mobile" href="https://css.seas.upenn.edu/project/covid-philadelphia/">COVID-Philadelphia</a>
                            </li>
                            <li class="sub-menu-list-mobile">
                                <a class="sub-item-mobile" href="https://css.seas.upenn.edu/project/common-sense/">Common Sense</a>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <a class="item-mobile" href='https://css.seas.upenn.edu/partnerships/'>Partners</a>
                    </li>
                    <li>
                        <a class="item-mobile" href='https://css.seas.upenn.edu/publications/'>Publications</a>
                    </li>
                    <li>
                        <a class="item-mobile" href='https://css.seas.upenn.edu/blog-news-events/'>News</a>
                    </li>
                </ul>
            </nav>
        </div>
    </div>
</header>

<style lang="scss">
    header {
        height: 50px;
        background-color: $css-lab-dark-blue;
        line-height: 23px;
        font-weight: 500;
        top: 0;
        width: 100%;
        box-shadow: 0 1px 0 rgb(0 0 0 / 10%);
        position: relative;
        z-index: 99999;

        @media (min-width: $bp-3) {
            height: 84px;
        }
    }

    .container {
        height: 100%;
        width: 80%;
        max-width: 1080px;
        margin: auto;
        text-align: left;
        position: relative;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .logo_container {
        height: 60%;
        width: auto;
    }

    .logo_anchor{
        display: block;
        height: 100%;
    }

    .logo_img {
        height: 100%;
        width: auto;
    }

    .nav {
        display: flex;
    }

    #et-top-navigation {
        display: none;
        height: 100%;

        @media (min-width: $bp-3) {
            display: block; 
            
        }
    }

    #top-menu-nav {
        height: 100%;
        display: flex;
        align-items: center;
    }

    #top-menu {
        margin: 0;
        height: 100%;
        display: flex;
        align-items: center;
    }


    .menu-item, .menu-item-has-children {
        display: inline-block;
        // align-items: center;
        font-size: 14px;
        padding-right: 22px;
        height: 100%;

        .sub-menu {
            position: absolute;
            padding: 20px 0;
            z-index: 9999;
            width: 240px;
            visibility: hidden;
            opacity: 0;
            background-color: $css-lab-dark-blue-transparent;
            border-top: 3px solid $css-lab-dark-red;
            box-shadow: 0 2px 5px rgba(0,0,0,.1);
            -moz-box-shadow: 0 2px 5px rgba(0,0,0,.1);
            -webkit-box-shadow: 0 2px 5px rgba(0,0,0,.1);
            -webkit-transform: translateZ(0);
            text-align: left;
        }
    }

    .menu-item-has-children:hover {
        .sub-menu {
            visibility: visible;
            opacity: 1;
            // margin: 29px 0 0 0;
        }
    }

    .menu-item-anchor {
        color: $light-grey;
        font-weight: 300;
        text-transform: uppercase;
        display: inline-flex;
        align-items: center;
        height: 100%;
    }

    .sub-menu-item-anchor {
        display: block;
        color: $light-grey;
        font-weight: 300;
        margin: 0 auto;
    }

    .sub-menu {
        > .menu-item {
            padding: 0 20px;
            line-height: 2em;

            a {
                width: 200px;
                padding: 6px 20px;
            }
        }
    }

    #et-top-navigation-mobile {
        display: block;
        height: 50%;

        @media (min-width: $bp-3) {
            display: none; 
        }
    }

    #top-menu-nav-mobile {
        height: 100%;

        .icon {
            width: 25px;
            height: 100%;
            padding: 2.5px;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            box-sizing: border-box;

            .line {
                height: 2px;
                background-color: $css-lab-light-blue;
                flex-grow: 0;
                flex-shrink: 0;
                pointer-events: none;
            }
        }
    }

    .nav-mobile {
        position: absolute;
        top: 50px;
        right: 0;
        left: 0;
        background-color: $css-lab-dark-blue;
        margin: 0;
        padding: 10%;
        list-style: none;

        li {
            margin: 15px 0;
        }

        a {
            color: $off-white;
            font-weight: 500;
            @include fs-base;
        }
    }

    .nav-mobile-hidden {
        display: none;
    }

    .nav-mobile-active {
        display: block;
    }

</style>