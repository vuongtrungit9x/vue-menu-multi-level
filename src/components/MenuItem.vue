<template>
    <ul class="dropdown-menu dropdown-dark" :aria-labelledby="parent">
        <li
            class="dropdown-item animate slideIn"
            :class="{'dropdown': checkHasChild(item)}"
            v-for="item in items "
            :key="item.id"
        >
            <a
                v-if="checkHasChild(item)"
                class="dropdown-toggle"
                :id="item.id"
                data-toggle="dropdown"
                aria-haspopup="true"
                aria-expanded="false"
            >
                <i :class="item.icon"/>
                {{item.name}}
            </a>
            <a v-else>
                <i :class="item.icon"/>
                {{item.name}}
            </a>
            <MenuItem v-if="item.children" :items="item.children" :parent="item.id"></MenuItem>
        </li>
    </ul>
</template>
<script>
import MenuItem from "./MenuItem.vue";
export default {
    name: "MenuItem",
    props: ["items", "parent"],
    components: {
        MenuItem
    },
    methods: {
        checkHasChild(item) {
            return item.children && item.children.length > 0;
        }
    }
};
</script>

            