<template>
    <v-btn
        tile
        block
        :color="(hover || id === current) ? '#182028' : 'transparent'"
        elevation="0"
        class="text-none jewel-button py-7"
        @mouseenter="hover = true"
        @mouseleave="hover = false"
        @click="selectJewel">
        <img 
            :src="jewelImg"
            :alt="jewelName"
            class="jewel-img mr-3">
        <span class="jewel-name" :class="`${hover ? 'underline' : ''} ${id == current ? 'jewel-selected' : ''}`"> {{ jewelName }}</span>
    </v-btn>
</template>

<script>
export default {
    props: {
        id: { //ID of the jewel
            required: true,
            type: String
        },
    },
    data() {
        return { //If the button is being hovered on
            hover: false
        }
    },
    computed: {
        jewelImg() { //Image of jewel
            return this.$store.getters.getJewelImg(this.id)
        },
        jewelName() { //Name of jewel
            return this.$store.getters.getJewelName(this.id)
        },
        current() { //Currently selected jewel
            return this.$store.getters.getCurrentJewel
        }
    },
    methods: {
        selectJewel: function() { //Informs parent of selected jewel, wipes current info
            this.$store.commit('setCurrentJewel', this.id)
            this.$store.commit('clearSeeds')
            this.$store.commit('clearConqs')
            this.$store.commit('clearLinks')
        }
    },
}
</script>

<style scoped>
.jewel-img {
  height: 3em;
  width: 3em;
  vertical-align: middle;
}
.jewel-button {
  justify-content: left;
}
.v-btn {
    border-radius: 0px;
}
.underline {
    text-decoration: underline;
}
.jewel-name {
    color: #E5E8EB;
    font-size: 18px;
    text-overflow: clip;
    white-space: break-spaces;
}
.jewel-selected {
    color: #10B77F;
}
</style>