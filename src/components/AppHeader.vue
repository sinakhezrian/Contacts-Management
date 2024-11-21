<template>
    <Header class="app-header">
        <h1 class="app-header-title">Contact Management</h1>
        <div class="app-header-input">
            <div class="app-header-search-icon">
                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0,0,256,256"
                    width="26px" height="26px" fill-rule="nonzero">
                    <g fill="#023e7d" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt"
                        stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0"
                        font-family="none" font-weight="none" font-size="none" text-anchor="none"
                        style="mix-blend-mode: normal">
                        <g transform="scale(5.12,5.12)">
                            <path
                                d="M21,3c-9.39844,0 -17,7.60156 -17,17c0,9.39844 7.60156,17 17,17c3.35547,0 6.46094,-0.98437 9.09375,-2.65625l12.28125,12.28125l4.25,-4.25l-12.125,-12.09375c2.17969,-2.85937 3.5,-6.40234 3.5,-10.28125c0,-9.39844 -7.60156,-17 -17,-17zM21,7c7.19922,0 13,5.80078 13,13c0,7.19922 -5.80078,13 -13,13c-7.19922,0 -13,-5.80078 -13,-13c0,-7.19922 5.80078,-13 13,-13z">
                            </path>
                        </g>
                    </g>
                </svg>
            </div>
            <input type="text" v-model="searchQuery" @input="onSearch" placeholder="Write to search ...">
        </div>
    </Header>
</template>

<script>
export default {
    name: "App-Header",
    props: ["searchValue"],
    emits: ["updateSearch"],
    data() {
        return {
            searchQuery: this.searchValue || "",
        };
    },
    methods: {
        onSearch() {
            this.$emit("updateSearch", this.searchQuery);
        },
    },
};
</script>

<style scoped>
.app-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 40px;
    background-color: #023e7d;
}

.app-header-title {
    color: #fff;
    letter-spacing: 2px;
}

.app-header-input {
    min-width: 300px;
    padding: 8px 10px;
    background: #fff;
    border-radius: 5px;
    display: flex;
    align-items: center;
}

.app-header-input input {
    padding: 5px;
    border: none;
    outline: none;
    width: 100%;
    letter-spacing: 0.7px;
    font-size: 15px;
}

.app-header-input input::placeholder {
    letter-spacing: 0.7px;
}

.app-header-search-icon {
    width: 34px;
    padding-top: 4px;
}
</style>