<template>
    <div class="app">
        <div class="components">
            <p class="title">アコーディオン1</p>
            <transition
               name="expand"
               @enter="enter"
               @after-enter="afterEnter"
               @leave="leave"
               @after-leave="afterLeave"
            >
                <div v-show="isShow" class="body">
                    <p>アコーディオン1の中身</p>
                    <p>アコーディオン1の中身</p>
                    <p>アコーディオン1の中身</p>
                </div>
            </transition>
        </div>
        <button v-on:click="isShow = !isShow">ボタン</button>
    </div>
</template>

<script>
export default {
    name: "Index",
    data() {
        return {
            isShow: true
        };
    },
    methods: {
        enter(el) {
            const height = getComputedStyle(el).height;
            el.style.width = null;
            el.style.position = null;
            el.style.visibility = null;
            el.style.height = '0';

            // Force repaint to make sure the
            // animation is triggered correctly.
            getComputedStyle(el).height;

            requestAnimationFrame(() => {
                el.style.height = height;
            });
        },
        afterEnter(el) {
            el.style.height = "auto";
        },
        leave(el) {
            const height = getComputedStyle(el).height;

            el.style.height = height;

            // Force repaint to make sure the
            // animation is triggered correctly.
            getComputedStyle(el).height;

            requestAnimationFrame(() => {
                el.style.height = "0";
            });
        },
        afterLeave(el) {
            el.style.height = "auto";
        }
    }
}
</script>

<style scoped lang="scss">
.components {
    width: 300px;
    text-align: center;
    font-weight: bold;
}
.title {
    padding: 0;
    margin: 0;
    border-color: #666;
    border-style: solid;
    background: #fff;
    font-size: 130%;
}
.body {
   border-color: #666;
   border-style: solid;
   background: #F0F0F0;
}
.expand-enter-active,
.expand-leave-active {
    transition: height .5s ease-in-out;
    overflow: hidden;
}

.expand-enter,
.expand-leave-to {
    height: 0;
}
</style>