<script setup lang="ts">
import { ref } from 'vue'

const fortunes = [
  "No snowflake in an avalanche ever <span>feels responsible</span>.",
  "A duel between three people is actually called a <span>truel</span>.",
  "Pigeon poop burns the retina <span>for 13 hours</span>.",
  "Sunsets on Mars are <span>blue</span>.",
  "Iguanas have <span>three eyes</span>.",
  "Sloths can hold their breath <span>longer than dolphins</span>.",
  "It’s impossible to hum while <span>holding your nose</span>.",
  "A flock of ravens is called an <span>“unkindness”</span> or a <span>“conspiracy”</span>",
  "It would only take one hour to <span>drive to space</span>.",
  "Adult cats only meow <span>at humans</span>.",
  "A “moonbow” is a rainbow that happens <span>at night</span>.",
  "Viagra can make flowers <span>stand up straight</span>.",
  "Butterflies will drink your <span>blood, sweat, and tears</span>.",
  "The Wizard of Oz’s full name is <span>Oscar Zoroaster Phadrig Isaac Norman Henkel Emmannuel Ambroise Diggs</span>.",
  "The word for Black Belt in Japanese translates to <span>“First Step”</span>.",
  "Vending machines are bigger threats to humanity <span>than sharks</span>.",
  "Cows have <span>best friends</span>.",
  "Orcas can learn to speak <span>Dolphin</span>."
]

const activeFortune = ref(fortunes[0])
const activeBox = ref("box1")

function swapNew(clicked: string) {
  const top = document.querySelector(".top")
  const mid = document.querySelector(".mid")
  const bot = document.querySelector(".bot")

  if (clicked == "box3" && activeBox.value === "box3") tellFortune()
  if (clicked == top?.id) return
  activeBox.value = clicked

  if (clicked == mid?.id) {
    mid?.classList.replace("mid", "top")
    top?.classList.replace("top", "bot")
    bot?.classList.replace("bot", "mid")
  }
  if (clicked == bot?.id) {
    bot?.classList.replace("bot", "top")
    top?.classList.replace("top", "bot")
  }
}

function tellFortune() {
  var randomNumber = Math.floor(Math.random() * fortunes.length)
  activeFortune.value = fortunes[randomNumber]
}
</script>

<template>
  <div id="box1" class="box mid" @click="swapNew('box1')">
    <div class="title">
      <h2><img src="@/assets/svg/hand-pointer-solid.svg" alt="icon-links">links</h2>
      <h3 class="switch">click to switch</h3>
    </div>
    <div class="content">
      <a class="com" href="https://facebook.com">Facebook</a>
      <a class="com" href="https://gmail.com">Gmail</a>
      <a class="com" href="https://youtube.com">Youtube</a>
      <a class="com" href="https://www.reddit.com">Reddit</a>
      <a class="com" href="https://unsplash.com/">Unsplash</a>
      <!-- <a class="org" href="https://4chan.org">4chan</a> -->
    </div>
  </div>

  <div id="box2" class="box top" @click="swapNew('box2')">
    <div class="title">
      <h2><img src="@/assets/svg/search-solid.svg" alt="icon search">search</h2>
      <h3 class="switch">click to switch</h3>
    </div>
    <div class="content">
      <form action="https://www.google.com/search">
        <p>Google</p><input type="text" name="q" placeholder="sharks & tornados ? ..." autofocus autocomplete="off" />
      </form>
      <form action="https://www.youtube.com/search">
        <p>Youtube</p><input type="text" name="q" placeholder="sharknado theme ..." autocomplete="off" />
      </form>
      <form action="https://en.wikipedia.org/w/index.php">
        <p>Wikipedia</p><input type="text" name="search" placeholder="sharknado cast ..." autocomplete="off" />
      </form>
      <form action="https://www.senscritique.com/recherche">
        <p>Senscritique</p><input type="text" name="query" placeholder="sharknado ..." autocomplete="off" />
      </form>
      <form action="https://www.discogs.com/search">
        <p>Discogs</p><input type="text" name="q" placeholder="sharknado OST ..." autocomplete="off" />
      </form>
    </div>
  </div>

  <div id="box3" class="box bot" @click="swapNew('box3')">
    <div class="title">
      <h2><img src="@/assets/svg/book-solid.svg" alt="icon facts"> facts</h2>
      <h3 :class="{ change: activeBox === 'box3', switch: activeBox !== 'box3' }">
        click to {{ activeBox === "box3" ? 'change' : 'switch' }}
      </h3>
    </div>
    <div class="content">
      <Transition mode="out-in">
        <p id="fortune" :key="activeFortune" v-html="activeFortune"></p>
      </Transition>
    </div>
  </div>
</template>

<style scoped lang="scss">
.box {
  position: absolute;
  width: 30rem;
  height: 30rem;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: var(--color1);
  padding: 2px;
  border: 2px solid var(--color3);
  transition: margin .3s ease-out;

  &:hover h2 {
    opacity: 1;
    visibility: visible;
  }
}

.top {
  margin-top: 6rem;
  margin-left: 6rem;
  z-index: 3;
}

.mid {
  z-index: 2;
}

.bot {
  margin-top: -6rem;
  margin-left: -6rem;
  z-index: 1;
}

.bot,
.mid,
#box3 {
  cursor: pointer;
}

.mid:hover,
.bot:hover {
  h2::after {
    opacity: 1;
    visibility: visible;
  }
}

a {
  text-decoration: none;
  color: var(--dark);
  font-size: 1rem;
  display: block;
  padding: 0.5rem 0;
  border-bottom: 2px solid var(--color3);
  width: 15rem;
  transition: padding-left .3s ease;

  &::after {
    transition: all .3s ease;
  }

  &:hover {
    padding-left: 1rem;

    &::after {
      content: ">";
      padding-left: 1rem;
      width: 1rem;
    }
  }
}

.com::after {
  content: ".com";
  color: var(--color3);
  font-family: "Cascadia semibold", monospace;
}

.org::after {
  content: ".org";
  color: var(--color3);
  font-family: "Cascadia semibold", monospace;
}

p {
  width: 15rem;
}

form {
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: center;
  width: 15rem;
}

input[type=text] {
  outline: none;
  border: none;
  border-bottom: 2px solid var(--color3);
  padding: 0.5rem 0;
  background-color: var(--color1);
  color: var(--dark);
  font-size: 1rem;
  width: 100%;
  transition: padding-left .3s ease;

  &:hover {
    padding-left: 1rem;
  }

  &::-webkit-input-placeholder,
  &::placeholder {
    color: var(--color3);
    font-size: 1rem;
  font-family: "Cascadia semibold", monospace;

    opacity: 1;
  }
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  gap: 1rem;
}

:deep(span) {
  color: var(--color3);
  font-family: "Cascadia semibold", monospace;
}

.title {
  position: absolute;
  top: 0;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transition: padding 0.3s;
  user-select: none;

  &:hover {
    padding: 0 1rem;
  }
}

h2 {
  display: flex;
  align-items: center;
  line-height: 1rem;
  font-size: 1rem;
  font-family: "Cascadia semibold", monospace;
  color: var(--dark);
  transition: all .3s ease;

  &::after {
    content: ">";
    opacity: 0;
    visibility: hidden;
    padding-left: 1rem;
    width: 1rem;
    color: var(--color3);
  }
}

h3 {
  line-height: 1rem;
  font-size: 1rem;
  margin: 1rem;
  font-family: "Cascadia semibold", monospace;
  color: var(--color3);
  transition: all .3s ease;
  opacity: 0;
  visibility: hidden;
}

img {
  height: 1rem;
  margin: 1rem;
}

.mid:hover .switch,
.bot:hover .switch,
.top:hover .change {
  opacity: 1;
  visibility: visible;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}


// media queries
@media (max-width: 40rem) {
  .box {
    width: calc(100vw - 4rem);
    height: calc(100vh - 10rem);
  }

  .top {
    margin-top: 6rem;
    margin-left: 0;
    // margin-left: 2rem;
  }

  .bot {
    margin-top: -6rem;
    margin-left: 0;
    // margin-left: -2rem;
  }

  .title:hover {
    padding: 0;
  }

  .switch {
    display: none;
  }

  .change {
    opacity: 1;
    visibility: visible;
  }

  a,
  p,
  form {
    width: 90%;
  }
}
</style>
