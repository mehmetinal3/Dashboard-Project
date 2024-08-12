<template>
  <div class="sidebars">
    <div :class="['pragmatic-text', { 'collapsed': isCollapsed }]">
      <img class="logo" src="https://pragmatic-linko.vercel.app/assets/logo-5e942556.svg">
      <p v-if="!isCollapsed" class="pragmatic">Pragmatic</p>
    </div>
    <div :class="['menu-bar', { 'collapsed': isCollapsed }]">
      <div v-for="product in products" :key="product.title || product.bigTitle">
        <ul class="menu-bar-list">
          <div v-if="product.bigTitle" :class="['title', { 'collapsed': isCollapsed}]">
            <span>{{ product.bigTitle }}</span>
          </div>
          <div v-else-if="product.titleChildren">
            <li :class="['menu-title', { 'collapsed': isCollapsed}]">
              <i :class="[product.icon, { 'collapsed': isCollapsed }]"></i>
              <span v-if="!isCollapsed" class="menu-items">{{ product.title }}</span>
              <i v-if="!isCollapsed" class="el-icon el-sub-menu__icon-arrow" @click="titleChildren(product, $event)" style="transform: none;"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024"><path fill="currentColor" d="M831.872 340.864 512 652.672 192.128 340.864a30.592 30.592 0 0 0-42.752 0 29.12 29.12 0 0 0 0 41.6L489.664 714.24a32 32 0 0 0 44.672 0l340.288-331.712a29.12 29.12 0 0 0 0-41.728 30.592 30.592 0 0 0-42.752 0z"></path></svg></i>
            </li>
             <div v-if="!isCollapsed" class="dashboard-children">
              <ul v-if="selectedProduct === product" class="menu-items-children">
                <li v-for="(child,index) in product.titleChildren" :key="index">
                  <div v-if="typeof child === 'object'">
                    <li v-for="(child2,index) in child" :key="index">
                      <div v-if="typeof child2 === 'object'">
                        <li v-for="(child3,index) in child2" :key="index">
                          <div v-if="typeof child3 === 'object'">
                            <li v-for="(child4,index) in child3" :key="index">
                              <!-- (4.1/4.2)' in çocukları -->
                              <div v-if="typeof child4 === 'object'">
                                <li v-for="(child5,index) in child4" :key="index">
                                    <div v-if="!isCollapsed" class="dashboard-children">
                                      <ul v-if="selectedProduct3 === product" class="menu-items-children3">
                                        <li :class="['menu-title', { 'collapsed': isCollapsed}]">
                                          <span v-if="!isCollapsed" class="menu-items">{{ child5 }}</span>
                                        </li>
                                      </ul>
                                    </div>
                                </li>
                              </div>
                              <!-- item four (4)'ün çocukları (4.1/4.2)-->
                              <div v-else>
                                <div v-if="!isCollapsed" class="dashboard-children">
                                  <ul v-if="selectedProduct2 === product" class="menu-items-children2">
                                    <li :class="['menu-title', { 'collapsed': isCollapsed}]">
                                      <span v-if="!isCollapsed" class="menu-items">{{ child4 }}</span>
                                      <i v-if="!isCollapsed" class="el-icon el-sub-menu__icon-arrow" @click="titleChildren3(product, $event)" style="transform: none;"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024"><path fill="currentColor" d="M831.872 340.864 512 652.672 192.128 340.864a30.592 30.592 0 0 0-42.752 0 29.12 29.12 0 0 0 0 41.6L489.664 714.24a32 32 0 0 0 44.672 0l340.288-331.712a29.12 29.12 0 0 0 0-41.728 30.592 30.592 0 0 0-42.752 0z"></path></svg></i>
                                    </li>
                                  </ul>
                                </div>
                              </div>
                            </li>
                          </div>
                          <!-- item four (4)'ün çocukları (4-3/4-7)-->
                          <div v-else>
                            <div v-if="!isCollapsed" class="dashboard-children">
                              <ul v-if="selectedProduct2 === product" class="menu-items-children2">
                                <li :class="['menu-title', { 'collapsed': isCollapsed}]">
                                <span v-if="!isCollapsed" class="menu-items">{{ child3 }}</span>
                                </li>
                              </ul>
                            </div>
                          </div>
                        </li>
                      </div>
                      <!-- item four (4) eklendi -->
                      <div v-else>
                        <li :class="['menu-title', { 'collapsed': isCollapsed}]" style="padding-left: 0px;">
                          <span v-if="!isCollapsed" class="menu-items">{{ child2 }}</span>
                          <i v-if="!isCollapsed" class="el-icon el-sub-menu__icon-arrow" @click="titleChildren2(product, $event)" style="transform: none;"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024"><path fill="currentColor" d="M831.872 340.864 512 652.672 192.128 340.864a30.592 30.592 0 0 0-42.752 0 29.12 29.12 0 0 0 0 41.6L489.664 714.24a32 32 0 0 0 44.672 0l340.288-331.712a29.12 29.12 0 0 0 0-41.728 30.592 30.592 0 0 0-42.752 0z"></path></svg></i>
                        </li>
                      </div>
                    </li>
                  </div>
                  <!-- ilk titleChildren'lar obje değilse -->
                  <div v-else>
                    {{ child }}
                  </div>
                </li>
              </ul>
            </div> 
          </div>
          <div v-else>
            <li :class="['menu-title', { 'collapsed': isCollapsed}]">
              <i :class="[product.icon, { 'collapsed': isCollapsed }]"></i>
              <span v-if="!isCollapsed" class="menu-items">{{ product.title }}</span>
            </li>
          </div>
        </ul>
      </div>
      <div :class="['collapse', { 'no-margin': isNoMargin }]" @click="toggleCollapse">
        <span>
          <i class="mdi" :class="isCollapsed ? 'mdi-unfold-more-vertical no-margin' : 'mdi-unfold-less-vertical'"></i>
          {{ isCollapsed ? '' : 'Collapse' }}
        </span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">

import { defineComponent, nextTick, PropType } from 'vue';
import { products } from '../data/products';
import '../assets/css/Header/flag.css'
import '../assets/css/Header/header.css'
import '../assets/css/Header/language.css'
import '../assets/css/Header/profile.css'
import '../assets/css/Menubar/menu-bar.css'

interface Product {
  icon?: string;
  title?: string;
  bigTitle?: string;
  titleChildren?: (string | {
    title: string;
    children: (string | {
      title: string;
      children: (string | {
        title: string;
        children: string[];
      })[];
    })[];
  })[];
}

export default defineComponent({
  props: {
    isCollapsed: {
      type: Boolean as PropType<boolean>,
      required: true,
    },
  },
  data() {
    return {
      products : products as Product[],
      selectedProduct: null as Product | null,
      rotatedSvg: null as SVGElement | null,
      selectedProduct2: null as Product | null,
      rotatedSvg2: null as SVGElement | null,
      selectedProduct3: null as Product | null,
      rotatedSvg3: null as SVGElement | null,
      isCollapsed: false,
      isNoMargin: false,
    }
  },
  methods: {
    handleTitleChildren(product: Product, event: Event, rotatedSvgKey: 'rotatedSvg' | 'rotatedSvg2' | 'rotatedSvg3', selectedProductKey: 'selectedProduct' | 'selectedProduct2' | 'selectedProduct3') {
      const target = event.currentTarget as HTMLElement;
      const svgElement = target.querySelector('svg') as SVGElement;

      const rotatedSvg = this[rotatedSvgKey] as SVGElement | null;
      const selectedProduct = this[selectedProductKey] as Product | null;

      if (rotatedSvg && rotatedSvg !== svgElement) {
        rotatedSvg.classList.remove('rotated');
      }

      this[selectedProductKey] = selectedProduct === product ? null : product;

      if (svgElement) {
        svgElement.classList.toggle('rotated');
        this[rotatedSvgKey] = svgElement.classList.contains('rotated') ? svgElement : null;
      }
  },

  titleChildren(product: Product, event: Event) {
  this.handleTitleChildren(product, event, 'rotatedSvg', 'selectedProduct');
  },

  titleChildren2(product: Product, event: Event) {
    this.handleTitleChildren(product, event, 'rotatedSvg2', 'selectedProduct2');
  },
  
  titleChildren3(product: Product, event: Event) {
    this.handleTitleChildren(product, event, 'rotatedSvg3', 'selectedProduct3');
  },


    
    toggleCollapse() {
      this.isCollapsed = !this.isCollapsed
      this.$emit('update:isCollapsed', this.isCollapsed);
      this.isNoMargin = !this.isNoMargin;
    },
  },
});
</script>

<style>

</style>


