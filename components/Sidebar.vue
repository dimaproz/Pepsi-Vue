<template>
  <nav
    id="nav"
    class="main-menu-wrap"
    :class="{ active: $store.state.sidebar }"
  >
    <div class="main-menu-head">
      <button v-if="user" type="button" @click.prevent="setModal('myaccount')">
        ОСОБИСТИЙ КАБІНЕТ
      </button>
      <button v-else type="button" @click.prevent="setModal('login')">
        Вхід
      </button>
      <button class="burger" @click="$store.dispatch('toggleSidebarState')">
        ×
      </button>
    </div>
    <div class="main-menu">
      <ul>
        <li>
          <a href="#" @click="focusInput()">Реєструй код</a>
        </li>
        <li>
          <a href="#" @click.prevent="setModal('winners')">Призи/переможці</a>
        </li>
        <li>
          <a href="#" @click.prevent="setInfoModal('rules')"
            >Офіційні правила</a
          >
        </li>
        <li>
          <a
            href="https://drive.google.com/file/d/1yLH0qSLUmh_EvfA1SFz2cdj5H6r-C9MF/view"
            target="_blank"
            >Запитання та відповіді</a
          >
        </li>
        <li @click="$store.dispatch('toggleSidebarState')">
          <NuxtLink to="/glass">Колекційні склянки</NuxtLink>
        </li>
        <li v-if="user">
          <a href="#" @click.prevent="$store.dispatch('logOut')">Вихід</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { mapActions } from 'vuex'
import EventHub from '~/plugins/EventHub'
export default {
  props: {
    user: {
      type: Object,
      default() {
        return null
      },
    },
  },
  methods: {
    ...mapActions({
      setModal: 'setModal',
      setInfoModal: 'setInfoModal',
    }),
    focusInput() {
      this.$store.dispatch('toggleSidebarState')
      EventHub.$emit('focusCodeInput')
    },
  },
}
</script>

<style lang="scss">
.main-menu-wrap {
  z-index: 900;
  padding: 40px 20px 100px 0;
  color: #fff;
  position: fixed;
  top: 0;
  right: 0;
  width: 450px;
  height: 100vh;
  transform: translateX(150%);
  transition: transform 0.3s;
  &.active {
    transform: translateX(0);
  }
}
.main-menu-wrap:after {
  content: '';
  position: absolute;
  left: -68px;
  top: -100px;
  right: -80px;
  bottom: -100px;
  background: #00225f;
  opacity: 0.9;
  z-index: -1;
  -webkit-transform: skewX(-6deg);
  -ms-transform: skewX(-6deg);
  transform: skewX(-6deg);
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
.main-menu-head {
  display: flex;
  align-items: center;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  font-size: 22px;
  text-transform: uppercase;
  margin-right: 95px;
  button {
    background: none;
    border: none;
    outline: none;
    color: #fff;
    font-family: 'Futura';
    font-size: 22px;
    text-transform: uppercase;
    cursor: pointer;
  }
  .burger {
    margin-left: 55px;
    font-family: 'Proxima Nova Condensed';
    font-size: 57px;
    line-height: 60px;
  }
}

.main-menu {
  font-size: 22px;
  text-transform: uppercase;
  //margin-top: 150px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 120px 0px;
  ul {
    margin-left: 57px;
    li {
      & + li {
        margin-top: 33px;
      }
      a:hover {
        color: #00aeef;
      }
    }
  }
}
@media all and (max-width: 1280px) {
  .main-menu-wrap {
    width: 360px;
    padding: 19px 20px 100px 0;
    &:after {
      left: -32px;
    }
  }
  .main-menu-head {
    margin-right: 50px;
    button {
      font-size: 17px;
    }
    .burger {
      font-size: 45px;
      margin-left: 27px;
    }
  }
  .main-menu {
    font-size: 17px;
    ul li + li {
      margin-top: 27px;
    }
  }
}
@media all and (max-width: 768px) {
  .main-menu-wrap {
    width: 340px;
    padding: 10px 20px 100px 0;
    &:after {
      left: -50px;
    }
  }
  .main-menu-head {
    font-size: 17px;
    margin-right: 22px;
    .burger {
      font-size: 45px;
      margin-left: 46px;
    }
  }
  .main-menu {
    font-size: 17px;
    ul {
      margin-left: 50px;
    }
  }
}
@media all and (max-width: 600px) {
  .main-menu-wrap {
    width: 100%;
    padding: 10px 20px 10px 40px;
    &:after {
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      transform: none;
    }
  }
  .main-menu-head {
    font-size: 17px;
    margin-right: 5px;
    button {
      font-size: 12px;
    }
    .burger {
      font-size: 37px;
      line-height: 20px;
      margin-left: 32px;
    }
  }
  .main-menu {
    font-size: 17px;
    padding: 0;
    ul {
      margin-left: 0px;
    }
  }
}
</style>
