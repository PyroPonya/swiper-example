<template>
  <div class="headerContainer">
    <header class="search">
      <input
        v-model="searchText"
        type="text"
        name="searchbar"
        placeholder=">huge searchbar"
      />
    </header>
    <header :class="{ 'headroom--unpinned': scrolled }" class="headroom navigation">
      <button v-for="(el, id) in props.hotkeys" :key="id">{{ el + 'btn' }}</button>
    </header>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';
export default {
  props: ['hotkeys'],
  setup(props) {
    // limitation for hotkey-bar hiding, px
    const limitPosition = 50;
    // hiding toggler
    const scrolled = ref(false);
    // memorized position
    const lastPosition = ref(0);
    // text in searchbar @TODO
    const searchText = ref('');
    // scroll handler for hiding hotkey-bar
    const handleScroll = () => {
      if (lastPosition.value < window.scrollY && limitPosition < window.scrollY) {
        scrolled.value = true;
        // move up
      }

      if (lastPosition.value > window.scrollY) {
        scrolled.value = false;
        // move down
      }

      lastPosition.value = window.scrollY;
    };
    // listeners
    onMounted(() => {
      window.addEventListener('scroll', handleScroll);
    });
    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll);
    });
    return {
      limitPosition,
      scrolled,
      lastPosition,
      searchText,
      handleScroll,
      props,
    };
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
  --elem-height: 3rem;
}
/*  */
.headerContainer {
  width: 100%;
  height: calc(var(--elem-height) * 2);
}
input[name='searchbar'] {
  width: 100%;
  height: 100%;
  font-size: 2rem;
  padding: 0.5rem;
}
header > button {
  width: 5rem;
  height: 2rem;
}
header > button:active {
  background-color: paleturquoise;
}
.search {
  width: 100%;
  height: var(--elem-height);
  background: cyan;
  position: fixed;
  z-index: 9;
}

.navigation {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: nowrap;
  gap: 1rem;
  width: 100%;
  height: var(--elem-height);
  top: var(--elem-height);
  background: rgb(36, 177, 182);
  position: fixed;
  z-index: 8;
}

.headroom {
  will-change: transform;
  transition: transform 200ms linear;
}
.headroom--pinned {
  transform: translateY(0%);
}
.headroom--unpinned {
  transform: translateY(-100%);
}
</style>
