<template>
  <div class="mobile-aside">
    <div class="user-head">
      <img src="../../static/user.jpeg" />
      <p>五角六芒星</p>

        <!-- <p
          @click="toogleTheme"
          class="scoll-btn theme">
            <i
              class="iconfont"
              :class="{
                'icon-dark': theme === 'light',
                'icon-light': theme === 'dark'
              }"
            ></i>
          </p> -->
    </div>
      <nav>
        <li
        v-for="(list, index) in nav"
        :key="index"
        class="nav-list "
        >
          <nuxt-link
            :to="list.path"
            exact>
              <span>{{ list.name }}</span>
          </nuxt-link>
        </li>
      </nav>
      <!-- <div class="aside-foot">
        <p class="mune">
          <nuxt-link to="/about">我</nuxt-link>
          <span class="hr"></span>
          <nuxt-link to="/">朋友</nuxt-link>
          <span class="hr"></span>
          <nuxt-link to="/">留言墙</nuxt-link>
          <span class="hr"></span>
          <nuxt-link to="/record">归档</nuxt-link>
        </p>
      </div> -->
  </div>
</template>

<script>
export default {
  name: 'mobile-aside',
  data () {
    return {
      nav: [
        // { path: '/', name: '首 页', icon: 'iconfont icon-home'},
        { path: '/about', name: 'About', icon: 'iconfont icon-home'},
        { path: '/', name: '朋友', icon: 'iconfont icon-read'},
        { path: '/record', name: '归 档', icon: 'iconfont icon-read'}
      ],
      theme: 'light'
    }
  },

  computed: {
    user () {
      return this.$store.state.options.adminInfo
    }
  },

  methods: {
    toogleTheme () {
      const isLight = document.body.id === 'light'

      this.theme = isLight ? 'dark' : 'light'

      document.body.id = this.theme
      window.localStorage.setItem('THEME', this.theme)
    }
  },

  mounted () {
    this.theme = window.localStorage.getItem('THEME') || 'light'
  }
}
</script>

<style scoped lang="scss">


.mobile-aside {
  position: relative;
  height: 100%;
  background: #ccc;
  >.user-head {
    padding: 3.5rem 1rem 1rem 1rem;
    text-align: center;

    >img {
      border-radius: 50%;
      width: 8rem;
      height: 10rem;
    }

    >p {
      margin-top: $mlg-pad;
      color: $black;
      font-size: 1.6rem;
    }


    .scoll-btn {
      display: block;
      margin-top: 2rem;
      text-align: center;
      line-height: 2rem;
      color: $black;
      cursor: pointer;

      i {
        font-size: $font-size-large;
      }
    }
  }
  > nav {
    margin-top: $mlg-pad;
    .nav-list {
      padding: 1rem;
      text-align: center;
    }
    a {
      margin-right: 0rem;
      padding: .5rem;
      color: $descript;

      i {
        margin-right: .8rem;
      }

      &:hover {
        color: $black;
      }
    }

    a.link-active {
      color: $black;
    }
  }

  > .aside-foot {
    position: absolute;
    bottom: $mlg-pad;
    left: 50%;
    width: 100%;
    font-size: $font-size-small;
    color: $disabled;
    text-align: center;
    transform: translate(-50%);
  }
}

</style>
