<script>
  import { onMount } from "svelte";
  import { fade } from "svelte/transition";
  import gsap from "gsap";
  let buttonNode;
  let formNode;
  let btn_size;
  let w;
  let h;
  let btn = {
    x: 0,
    y: 0
  };
  let rnd = {
    btwn: function(min, max) {
      return Math.floor(Math.random() * (max - min) + min);
    }
  };
  let show = false;
  let email = "";
  const PLACEHOLDER_DEFAULT = "youremail@email.com";
  let placeholder = PLACEHOLDER_DEFAULT;

  onMount(() => {
    btn_size = buttonNode.getBoundingClientRect();
    console.log(btn_size);
    w = document.body.clientWidth - btn_size.width;
    h = document.body.clientHeight - btn_size.height;
    btn.x = h / 2;
    btn.y = w / 2;
    gsap.set(buttonNode, {
      left: btn.y,
      top: btn.x
    });
  });

  function updateBtn(shiftX, shiftY) {
    shiftX = !!shiftX ? shiftX : 0;
    shiftY = !!shiftY ? shiftY : 0;

    gsap.to(buttonNode, {
      left: btn.y + shiftY,
      top: btn.x + shiftX,
      duration: 0.5,
      ease: "elastic.out(1, 0.5)"
    });
  }

  function handleMouseOver() {
    btn.x = rnd.btwn(0, h);
    btn.y = rnd.btwn(0, w);
    updateBtn();
  }

  function handleResize() {
    w = document.body.clientWidth - btn_size.width;
    h = document.body.clientHeight - btn_size.height;
    btn.x = h / 2;
    btn.y = w / 2;
    updateBtn();
  }

  function handleSubmit(e) {
    if (email.length < 1) return;
    let formData = new FormData(formNode);
    fetch("/", {
      method: "POST",
      headers: { "Content-Type": "application/x-www-form-urlencoded" },
      body: new URLSearchParams(formData).toString()
    })
      .then(() => {
        email = "";
        placeholder = "Successfully removed.";
        setTimeout(() => {
          show = false;
        }, 1500);
      })
      .catch(error => alert(error));
  }
</script>

<style>
  div {
    position: absolute;
    width: 100%;
    height: 100%;
  }
  button.unsubscribe {
    background-image: url("data:image/svg+xml,%3Csvg width='259' height='66' viewBox='0 0 259 66' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cg filter='url(%23filter0_di)'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M0 0V64H257V0H0Z' fill='url(%23paint0_linear)'/%3E%3Cpath d='M256.5 63.5H0.5V0.5H256.5V63.5Z' stroke='%23131313'/%3E%3C/g%3E%3Cg filter='url(%23filter1_d)'%3E%3Cpath d='M46.0664 40V37.375H53.9414V40H46.0664ZM43.4414 37.375V21.625H46.0664V37.375H43.4414ZM53.9414 37.375V21.625H56.5664V37.375H53.9414Z' fill='%23181819'/%3E%3Cpath d='M69.6914 40V29.5H72.3164V40H69.6914ZM59.1914 40V26.875H61.8164V29.5H64.4414V32.125H61.8164V40H59.1914ZM64.4414 29.5V26.875H69.6914V29.5H64.4414Z' fill='%23181819'/%3E%3Cpath d='M74.9414 40V37.375H85.4414V40H74.9414ZM85.4414 37.375V34.75H88.0664V37.375H85.4414ZM77.5664 34.75V32.125H85.4414V34.75H77.5664ZM74.9414 32.125V29.5H77.5664V32.125H74.9414ZM77.5664 29.5V26.875H85.4414V29.5H77.5664Z' fill='%23181819'/%3E%3Cpath d='M93.3164 40V37.375H101.191V40H93.3164ZM90.6914 37.375V26.875H93.3164V37.375H90.6914ZM101.191 37.375V26.875H103.816V37.375H101.191Z' fill='%23181819'/%3E%3Cpath d='M116.941 37.375V29.5H119.566V37.375H116.941ZM111.691 29.5V26.875H116.941V29.5H111.691ZM106.441 40V21.625H109.066V29.5H111.691V32.125H109.066V37.375H116.941V40H106.441Z' fill='%23181819'/%3E%3Cpath d='M122.191 40V37.375H132.691V40H122.191ZM132.691 37.375V34.75H135.316V37.375H132.691ZM124.816 34.75V32.125H132.691V34.75H124.816ZM122.191 32.125V29.5H124.816V32.125H122.191ZM124.816 29.5V26.875H132.691V29.5H124.816Z' fill='%23181819'/%3E%3Cpath d='M140.566 40V37.375H148.441V40H140.566ZM148.441 37.375V34.75H151.066V37.375H148.441ZM137.941 37.375V29.5H140.566V37.375H137.941ZM140.566 29.5V26.875H148.441V29.5H140.566Z' fill='%23181819'/%3E%3Cpath d='M164.191 32.125V29.5H166.816V32.125H164.191ZM153.691 40V26.875H156.316V29.5H158.941V32.125H156.316V40H153.691ZM158.941 29.5V26.875H164.191V29.5H158.941Z' fill='%23181819'/%3E%3Cpath d='M169.441 40V37.375H172.066V29.5H169.441V26.875H174.691V37.375H177.316V40H169.441ZM172.066 24.25V21.625H174.691V24.25H172.066Z' fill='%23181819'/%3E%3Cpath d='M190.441 37.375V29.5H193.066V37.375H190.441ZM185.191 29.5V26.875H190.441V29.5H185.191ZM179.941 40V21.625H182.566V29.5H185.191V32.125H182.566V37.375H190.441V40H179.941Z' fill='%23181819'/%3E%3Cpath d='M198.316 40V37.375H206.191V40H198.316ZM195.691 37.375V29.5H198.316V32.125H206.191V29.5H208.816V34.75H198.316V37.375H195.691ZM198.316 29.5V26.875H206.191V29.5H198.316Z' fill='%23181819'/%3E%3C/g%3E%3Cdefs%3E%3Cfilter id='filter0_di' x='0' y='0' width='259' height='66' filterUnits='userSpaceOnUse' color-interpolation-filters='sRGB'%3E%3CfeFlood flood-opacity='0' result='BackgroundImageFix'/%3E%3CfeColorMatrix in='SourceAlpha' type='matrix' values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0'/%3E%3CfeOffset dx='1' dy='1'/%3E%3CfeGaussianBlur stdDeviation='0.5'/%3E%3CfeColorMatrix type='matrix' values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0'/%3E%3CfeBlend mode='normal' in2='BackgroundImageFix' result='effect1_dropShadow'/%3E%3CfeBlend mode='normal' in='SourceGraphic' in2='effect1_dropShadow' result='shape'/%3E%3CfeColorMatrix in='SourceAlpha' type='matrix' values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0' result='hardAlpha'/%3E%3CfeOffset dx='2' dy='2'/%3E%3CfeComposite in2='hardAlpha' operator='arithmetic' k2='-1' k3='1'/%3E%3CfeColorMatrix type='matrix' values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 0.71905 0'/%3E%3CfeBlend mode='normal' in2='shape' result='effect2_innerShadow'/%3E%3C/filter%3E%3Cfilter id='filter1_d' x='43.4414' y='21.625' width='165.375' height='19.375' filterUnits='userSpaceOnUse' color-interpolation-filters='sRGB'%3E%3CfeFlood flood-opacity='0' result='BackgroundImageFix'/%3E%3CfeColorMatrix in='SourceAlpha' type='matrix' values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0'/%3E%3CfeOffset dy='1'/%3E%3CfeColorMatrix type='matrix' values='0 0 0 0 1 0 0 0 0 0.999937 0 0 0 0 1 0 0 0 0.498162 0'/%3E%3CfeBlend mode='normal' in2='BackgroundImageFix' result='effect1_dropShadow'/%3E%3CfeBlend mode='normal' in='SourceGraphic' in2='effect1_dropShadow' result='shape'/%3E%3C/filter%3E%3ClinearGradient id='paint0_linear' x1='0' y1='0' x2='0' y2='64' gradientUnits='userSpaceOnUse'%3E%3Cstop stop-color='%23DADADA'/%3E%3Cstop offset='0.930671' stop-color='%23DADADA'/%3E%3Cstop offset='1' stop-color='%23525151'/%3E%3C/linearGradient%3E%3C/defs%3E%3C/svg%3E%0A");
    outline: none;
    text-indent: -9999px;
    width: 9.5625rem;
    height: 2.4375rem;
    background-size: contain;
    background-repeat: no-repeat;
    border: none;
    position: absolute;
    cursor: pointer;
    z-index: 1;
  }
  p {
    margin: 0;
    padding: 0;
    pointer-events: none;
    color: #bfbfbf;
  }
  p.top {
    font-size: 1.125rem;
    margin-left: 3.1875rem;
    position: absolute;
    top: 1.9375rem;
  }
  p.bottom {
    font-size: 0.8125rem;
    max-width: 39.1875rem;
    margin-left: 3.1875rem;
    position: absolute;
    bottom: 5.75rem;
  }
  a.red {
    color: #d39393;
  }
  a {
    pointer-events: auto;
  }
  a:hover {
    text-decoration: none;
  }

  .email-form {
    width: 100%;
    height: 100%;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #fdfdfb;
    flex-direction: column;
  }

  .email-form p {
    font-size: 1.5rem;
    color: #4f4c4c;
    margin-bottom: 5.6875rem;
  }

  .email-form input {
    border: 3px solid #ebeaea;
    width: 29.4375rem;
    height: 3.6875rem;
    color: #4f4c4c;
    font-size: 1.5rem;
    outline: 0;
    text-indent: 1rem;
  }

  .email-form input::placeholder {
    color: #bfbfbf;
  }

  .email-form button {
    background: #ff5316;
    border-radius: 6px;
    border: none;
    outline: 0;
    color: #fdfdfb;
    font-size: 1.125rem;
    padding: 1.4rem 5rem;
    text-transform: uppercase;
    margin-left: 2.25rem;
    transition: opacity 0.3s;
  }

  .email-form button:hover {
    opacity: 0.7;
  }

  @media only screen and (max-width: 39.1875rem) {
    /* CSS rules here */
    p.top {
      width: 80vw;
    }
    p.bottom {
      width: 80vw;
    }
    .email-form {
      margin: 1rem;
    }
    .email-form input {
      width: 90%;
    }
    .email-form button {
      margin-left: 0;
      margin-top: 2rem;
      width: 92%;
    }
  }
</style>

<svelte:head>
  <title>
    DIKO - UNSUBSCRIBE (Please unsubscribe, we have plenty of subscribers.)
  </title>
</svelte:head>
<svelte:window on:resize={handleResize} />

<div>
  <p class="top">
    Part of the
    <b>Work Smarder™ Series</b>
    from
    <b>DIKO</b>
  </p>
  <button
    class="unsubscribe"
    bind:this={buttonNode}
    on:mouseover={handleMouseOver}
    on:click={handleMouseOver}>
    unsubscribe
  </button>
  <p class="bottom">
    For god’s sake don’t unsubscribe. We’ll even give you our Unsubscribable
    Unsubscribe Button™ to use with your own not-a-newsletter that you can
    <a class="red" download href="archive.zip">download here.</a>
    If that’s not enough to make you stay and you still want to unsubscribe,
    please submit a 1000-word essay explaining the reasons why or
    <a
      href=""
      on:click|preventDefault={() => {
        show = !show;
      }}>
      simply opt out by clicking here.
    </a>
  </p>
</div>
{#if show}
  <div
    class="email-form"
    transition:fade={{ duration: 200 }}
    on:click|preventDefault|self={() => {
      show = !show;
    }}>
    <p>Enter your email we will remove you from our mailing list.</p>
    <form
      name="unsubscribe"
      on:submit|preventDefault={handleSubmit}
      bind:this={formNode}>
      <input type="hidden" name="form-name" value="unsubscribe" />
      <input type="email" {placeholder} name="email" bind:value={email} />
      <button type="submit">Send</button>
    </form>
  </div>
{/if}
