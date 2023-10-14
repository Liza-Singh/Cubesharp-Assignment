<template>
    <v-navigation-drawer class="sidebar" v-model="drawer" app color="blue" mini-variant mini-variant-width="80">
        <v-list flat class="mt-16">
            <v-list-item-group v-model="selectedItem">
                <v-list-item v-for="(item, i) in items" :key="i" :ripple="false">
                    <v-list-item-icon>
                        <v-icon class="topIcons" v-html="item.icon" color="white"></v-icon>
                    </v-list-item-icon>
                </v-list-item>
            </v-list-item-group>
        </v-list>
        <div class="lowerIcons">
            <br />
            <v-icon color="white" class="fa-regular fa-circle-user"></v-icon>
        </div>
    </v-navigation-drawer>
</template>
  
<script>
import '@fortawesome/fontawesome-free/css/all.css';
export default {
    data: () => ({
        drawer: null,
        selectedItem: 0,
        items: [
            { icon: '<i class="fa-regular fa-square-plus"></i>' },
            { icon: '<i class="fa fa-calendar @click="toggleCalendar"></i>' },
            { icon: '<i class="fa-regular fa-bell"></i>' },
            { icon: '<i class="fa-regular fa-note-sticky"></i>' },
            { icon: '<i class="fa-solid fa-gear"></i>' },
        ],

    }),
    methods: {
        toggleCalendar() {
            this.$emit('toggle-calendar');
        },
    },
};
</script>
  
  
<style scoped>
* {
    margin: 0%;
    padding: 0%;
    outline: none;
    border: none;
    box-sizing: border-box;

}

.sidebar {
    display: flex;
    min-height: 100%;
    background-color: #F0F0F0;
    position: absolute;
    overflow: hidden;
    transition: width 0.2s linear;
    font-size: 25px;
}

.topIcons {

    display: flex;
    padding: 20px;
}

.topIcons:hover {
    background: #6499E9;

}

.lowerIcons {
    position: absolute;
    bottom: 20px;
    margin-left: auto;
    margin-right: auto;
    left: 0;
    right: 0;
    text-align: center;
    padding-bottom: 20px;

}

.lowerIcons:hover {
    background: #6499E9;
}

.border {
    border: red;

}

.individualIcon {
    padding: 50px;
}

.v-list-item-group .v-list-item--active {
    color: white !important;
}

.icons {
    text-align: center;
}</style>