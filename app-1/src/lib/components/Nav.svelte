<script>
     import { page } from '$app/stores';
   import { afterNavigate } from '$app/navigation';


   afterNavigate(() => {
   const oldPage = document.querySelector('.active');
   const activPage = document.querySelector('[href="' + 
                     $page.url.pathname + '"]');
 
   if (oldPage != null && activPage != null) {
       oldPage.classList.remove('active');
   }
 
   if (activPage != null && !activPage.classList.contains('active'))
       activPage.classList.add('active');
});



    let displayMenu = 'none';
    let show = false;
  
    $: displayMenu = show ? 'block' : 'none';
 </script>
 
<nav>
    <button on:click={()=>show = !show}>
        <img src="/btn-menu.svg" alt="menu btn" height="25" />
    </button>
    <ul on:click={()=>show = false} style="--nav-ul-display: {displayMenu}">
        <li><a href="/">Hem</a></li>
        <li><a href="/course">Kurs</a></li>
        <li><a href="/about">Om</a></li>
    </ul>
</nav>

<style lang="scss">
    nav {
        display: flex;
        color: #e2e3db;
        font-size: medium;
        justify-content: end;
        margin-right: var(--margin-l);
        font-size: medium;
        z-index: 10;
        button {
            border: 0;
            background: transparent;
            display: none;
            padding: 0;
        }
        ul { 
            list-style-type: none;
            overflow: hidden;
            background-color: #333;
            display: flex;
            z-index: 100;
            li {
                background-color: #333;
                color: #e2e3db;

                a {
                    display: block;
                    text-align: center;
                    padding: 0.8rem 1.6rem;
                    text-decoration: none;
                    font-weight: 600;
                    margin: 0;
                    color: inherit;

                    &.active {
                        background-color: #ff3e00;
                    }
                    &:hover:not(.active) {
                        background-color: #111;
                        color: #fff;
                    }
                }
            }
        }
    }
    @media only screen and (max-width: 768px) {
        nav {
            margin-right: var(--margin-m);
            button {
                display: inline;
                cursor: pointer;
            }
            ul {
                display: var(--nav-ul-display, none);
                position: absolute;
                top: 4rem;
                width: 50%;
                li {
                    display: block;
                }
            }
        }
    }
    @media only screen and (max-width: 420px) {
        nav {
            margin-right: var(--margin-s);
        }
    }

:global(nav li a.active) {
    background-color: #ff3e00;
}
</style>
