<template>
  <StackLayout :width="width" class="bg-white" @tap="tapClick">
    <GridLayout columns="*, 30" rows="*" :class="headerClass" v-if="!hidden">
      <slot class="slot" name="header" >
        <Label col="0" :class="headerClassBtn" textWrap="true" :textAlignment="textAlignment" :text="title" />
      </slot>
      <slot class="slot" name="button" >
        <vn-btn col="1" :label="''" :class="closeClass"
            @tap="doCloseable" 
            :tintColor="tintColor"
            :appendIcon="showPanel ? closeIcon : closeIconActive" style="padding-top: -8px;">
        </vn-btn>
      </slot>
    </GridLayout>
    <GridLayout v-show="showPanel" rows="auto" iosOverflowSafeArea="false">
        <slot class="slot" name="content"></slot>
    </GridLayout>
  </StackLayout>
</template>
<script>
export default {
  data() {
    return {
      showPanel: true,
      closeableIcon: '~/assets/svg/keyboard_arrow_down/black.svg'
    };
  },
  props: {
    title: String,
    width: String,
    height: String,
    alignment: String,
    closeable: {
      type: Boolean,
      default: true
    },
    tintColor: {
      type: String,
      default: ''
    },
    width: String,
    hidden: Boolean,
    radius: {
      type: String,
      default: ''
    },
    headerClass: {
      type: String,
      default: 'h-3'
    },
    headerClassBtn: {
      type: String,
      default: 'text-left text-gray-900 text-lg p-2 pl-4 fa font-semibold'
    },
    textAlignment: {
      type: String,
      default: 'left'
    },
    closeClass: {
      type: String,
      default: 'hidden'
    },
    closeIcon: {
      type: String,
      default: 'keyboard_arrow_down'
    },
    closeIconActive: {
      type: String,
      default: 'keyboard_arrow_up'
    }
  },
  mounted() {
    let vm = this;
    vm.$nextTick(function() {
      if (vm.showPanel) {
        vm.closeableIcon = '~/assets/svg/keyboard_arrow_up/black.svg';
      } else {
        vm.closeableIcon = '~/assets/svg/keyboard_arrow_down/black.svg';
      }
    })
  },
  methods: {
    doCloseable() {
      if (this.closeable) {
        this.showPanel = !this.showPanel
      }
    },
    tapClick() {
      this.$emit('tap')
      
    }
  }
};
</script>
<style>
  .hidden {
    display: none;
  }
</style>