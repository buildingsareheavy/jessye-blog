<template>
  <div id="app">
    <header class="header">
      <div class="header__left">
        <Logo v-if="showLogo"/>
        <ToggleTheme/>
      </div>

      <div class="header__right">
        <g-link class="navigation" to="/">Videos</g-link>
        <g-link class="navigation" :to="{ name: 'info' }">Info</g-link>
        <!-- <g-link class="navigation" :to="{ name: 'interviews' }">Interviews</g-link> -->
      </div>
    </header>
    <transition name="fade" appear>
      <main class="main">
        <slot/>
      </main>
    </transition>
    <footer class="footer">
      <span class="footer__copyright">Copyright © {{ new Date().getFullYear() }}.</span>
      <span class="footer__links">
        Made by
        <a href="//buildingsareheavy.com">Ethan Barrett</a>
      </span>
    </footer>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import ToggleTheme from "~/components/ToggleTheme.vue";

export default {
  props: {
    showLogo: { default: true }
  },
  components: {
    Logo,
    ToggleTheme
  }
};
</script>

<style lang="scss">
@font-face {
  font-family: "Questa";
  src: url("../assets/fonts/Questa_Sans.woff");
}

@font-face {
  font-family: "Museo";
  src: url("../assets/fonts/Museo_Slab.woff");
}

*,
a,
p,
span,
footer {
  font-family: "Questa", monospace;
}

h1,
h2,
h3,
h4,
h5,
h6,
p.video-name {
  font-family: "Museo", monospace;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  min-height: var(--header-height);
  padding: 0 calc(var(--space) / 2);
  top: 0;
  z-index: 10;
  background: var(--bg-content-color);
  box-shadow: 1px 1px 15px 0 rgba(0, 0, 0, 0.03);

  &__left,
  &__right {
    display: flex;
    align-items: center;
  }

  .navigation {
    padding: 0 1rem;
    text-decoration: none;
    color: currentColor;

    &.active--exact.active {
      border-bottom: 1px solid var(--body-color);
      margin-bottom: -1px;
      transition: 0.2s all;
    }
  }

  @media screen and (min-width: 1300px) {
    //Make header sticky for large screens
    position: sticky;
    width: 100%;
  }
}

.main {
  margin: 0 auto;
  padding: 1.5vw 15px 0;
}

.footer {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: calc(var(--space) / 2);
  text-align: center;
  font-size: 0.8em;

  > span {
    margin: 0 0.35em;
  }

  a {
    color: currentColor;
  }
}

.fade-enter {
  opacity: 0;
  &-active {
    transition: opacity 1s;
  }
}
</style>
