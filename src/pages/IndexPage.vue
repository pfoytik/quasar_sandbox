<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md q-gutter-sm">
      <q-avatar>
        <img src="https://cdn.quasar.dev/img/avatar.png" />
        <q-tooltip
          :delay="1500"
          anchor="center middle"
          self="center middle"
          class="bg-black"
        >
          <q-banner>
            <template v-slot:avatar>
              <q-img src="~./trident.png" style="width: 50px; height: 50px" />
            </template>
            <p style="color: black">Profile information</p>
            <q-btn color="white" text-color="black" label="Standard"> </q-btn>
          </q-banner>
        </q-tooltip>
      </q-avatar>
    </div>

    <q-img
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    >
      <q-tooltip
        :delay="1500"
        anchor="center middle"
        self="center middle"
        class="bg-black"
      >
        <q-banner>
          <template v-slot:avatar>
            <q-img src="~./trident.png" style="width: 50px; height: 50px" />
          </template>
          <p style="color: black">Profile information</p>
          <q-btn color="white" text-color="black" label="Standard"> </q-btn>
        </q-banner>
      </q-tooltip>
    </q-img>

    <div class="q-pa-md q-gutter-sm">
      <q-btn color="white" text-color="black" label="Standard">
        <q-tooltip :delay="1500">
          <q-banner>
            <template v-slot:avatar>
              <q-icon name="signal_wifi_off" color="primary" />
            </template>
            You have lost connection to the internet. This app is offline.
          </q-banner>
        </q-tooltip>
      </q-btn>
    </div>

    <div class="q-pa-md">
      <q-btn-dropdown auto-close color="primary" label="Dropdown Button" v-model="menu" @mouseover="menuOver = true" @mouseout="menuOver = false">
        <img src="https://cdn.quasar.dev/img/avatar.png" />
        <q-list @mouseover="listOver = true" @mouseout="listOver = false">
          <q-item clickable>
            <div class="column">
              <div class="text-h6 q-mb-md">Settings</div>
              <q-toggle v-model="mobileData" label="Use Mobile Data" />
              <q-toggle v-model="bluetooth" label="Bluetooth" />
            </div>

            <q-separator vertical inset class="q-mx-lg" />

            <div class="column items-center">
              <q-avatar size="72px">
                <img src="https://cdn.quasar.dev/img/avatar4.jpg">
              </q-avatar>

              <div class="text-subtitle1 q-mt-md q-mb-xs">John Doe</div>

              <q-btn
                color="primary"
                label="Logout"
                push
                size="sm"
                v-close-popup
              />
            </div>
          </q-item>

          <q-item clickable>
            <q-item-section>
              <q-item-label>Videos</q-item-label>
            </q-item-section>
          </q-item>

          <q-item clickable>
            <q-item-section>
              <q-item-label>Articles</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-btn-dropdown>
    </div>

    <div class="q-pa-md">
      <q-btn color="purple" label="Account Settings" v-model="showing" @mouseover="menuOver = true" @mouseout="menuOver = false">
        <q-menu @mouseover="listOver = true" @mouseout="listOver = false">
          <div class="row no-wrap q-pa-md">
            <div class="column">
              <div class="text-h6 q-mb-md">Settings</div>
              <q-toggle v-model="mobileData" label="Use Mobile Data" />
              <q-toggle v-model="bluetooth" label="Bluetooth" />
            </div>

            <q-separator vertical inset class="q-mx-lg" />

            <div class="column items-center">
              <q-avatar size="72px">
                <img src="https://cdn.quasar.dev/img/avatar4.jpg">
              </q-avatar>

              <div class="text-subtitle1 q-mt-md q-mb-xs">John Doe</div>

              <q-btn
                color="primary"
                label="Logout"
                push
                size="sm"
                v-close-popup
              />
            </div>
          </div>
        </q-menu>
      </q-btn>
    </div>

    <div class="q-pa-md">
      <q-avatar clickable color="red" label="account" v-model="menu" @mouseover="menuOver = true" @mouseout="menuOver = false">
        <img src="https://cdn.quasar.dev/img/avatar.png" />
        <q-menu @mouseover="listOver = true" @mouseout="listOver = false">
          <div class="row no-wrap q-pa-md">
            <q-item clickable>
              <div class="column">
                <div class="text-h6 q-mb-md">Settings</div>
                <q-toggle v-model="mobileData" label="Use Mobile Data" />
                <q-toggle v-model="bluetooth" label="Bluetooth" />
              </div>

              <q-separator vertical inset class="q-mx-lg" />

              <div class="column items-center">
                <q-avatar size="72px">
                  <img src="https://cdn.quasar.dev/img/avatar4.jpg">
                </q-avatar>

                <div class="text-subtitle1 q-mt-md q-mb-xs">John Doe</div>

                <q-btn
                  color="primary"
                  label="Logout"
                  push
                  size="sm"
                  v-close-popup
                />
              </div>
            </q-item>

            <q-item clickable>
              <q-item-section>
                <q-item-label>Videos</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable>
              <q-item-section>
                <q-item-label>Articles</q-item-label>
              </q-item-section>
            </q-item>
          </div>
        </q-menu>
      </q-avatar>
    </div>

  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { ref } from 'vue';
import { debounce } from 'quasar';

export default defineComponent({
  setup() {
    return {
      menuOpen: ref(false),
      showing: ref(false),
      menu: ref(false),
      menuOver: ref(false),
      listOver: ref(false),
      mobileData: ref(true),
      bluetooth: ref(false)
    };
  },
  methods: {
    onItemClick () {
      console.log('Clicked on an Item')
    },
    debounceFunc: debounce(function () {
      this.checkMenu();
    }, 1000),
    checkMenu() {
      if (this.menuOver || this.listOver) {
        this.menu = true;
        this.showing = true;
        console.log("What is showing "+ this.showing)
      }
      else {
        this.menu = false;
        this.showing = false;
      }
    },
  },
  watch: {
    menuOver() {
      return this.debounceFunc();
    },
    listOver() {
      return this.debounceFunc();
    },
    mouseOver() {
      return this.debounceFunc();
    },
  },
  name: "IndexPage",
  });


</script>
