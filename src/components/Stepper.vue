<template>
    <v-sheet class="stepper-box" width="50" height="50">
        <v-icon
            v-if="icon"
            size="50"
            color="rgba(255,255,255,0.2)"
            class="background-icon"
            v-bind:style="{ top: iconoffset + 'px' }"
            ref="backgroundicon"
        >
            {{icon}}
        </v-icon>
        <p class="stepper-count">{{ count.val }}</p>
        <v-hover>
            <template v-slot:default="{ hover }">
                <div class="changecount add" @click.stop="updateCount(1)">
                    <v-fade-transition>
                        <v-overlay
                            v-if="hover"
                            absolute
                            color="#036358"
                        >
                            <v-icon>mdi-chevron-up</v-icon>
                        </v-overlay>
                    </v-fade-transition>
                </div>
            </template>
        </v-hover>

        <v-hover>
            <template v-slot:default="{ hover }">
                <div class="changecount subtract" @click.stop="updateCount(-1)">
                    <v-fade-transition>
                        <v-overlay
                            v-if="hover"
                            absolute
                            color="#036358"
                        >
                            <v-icon>mdi-chevron-down</v-icon>
                        </v-overlay>
                    </v-fade-transition>
                </div>
            </template>
        </v-hover>

     </v-sheet>
</template>

<script>
export default {
    props: ['count', 'icon', 'iconoffset'],
    methods: {
        updateCount(inc) {
            this.count.val = this.count.val + inc
            this.$root.$data.sendGameData()
        }
    }
}
</script>

<style lang="scss" >

div.stepper-box {
    display: inline-block;
    margin: 0px;
    position: relative;
}

p.stepper-count {
    margin: 0;
    padding: 0;
    text-align: center;
    font-size: 1.3em;
    font-weight: bold;
    line-height: 50px;
    width: 50px;
    top: 0px;
    position: absolute;
    z-index: 1;
}

.stepper-box {
    position: relative;

    .changecount {
        position: absolute;
        width: 50px;
        height: 25px;
        box-sizing: border-box;
        z-index: 2;
        cursor: pointer;
    }

    .add {
        top: 0;
    }

    .subtract {
        top: 25px;
    }

    .background-icon {
        position: absolute;
        background-color: transparent;
        z-index: 0;
    }
}


</style>