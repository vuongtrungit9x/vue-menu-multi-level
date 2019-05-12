
<template>
    <div class="navbar navbar-expand-md navbar-dark bg-dark mb-4" role="navigation">
        <button
            class="navbar-toggler"
            type="button"
            data-toggle="collapse"
            data-target="#navbarCollapse"
            aria-controls="navbarCollapse"
            aria-expanded="false"
            aria-label="Toggle navigation"
        >
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarCollapse">
            <ul class="navbar-nav mr-auto animate slideIn">
                <li
                    v-for="item in menus "
                    :key="item.id"
                    class="nav-item"
                    :class="{'active': item.id == activeID,
                    'dropdown':item.children && item.children.length >0}"
                >
                    <a
                        v-if="item.children && item.children.length >0"
                        class="nav-link dropdown-toggle"
                        :id="item.id"
                        data-toggle="dropdown"
                        aria-haspopup="true"
                        aria-expanded="true "
                        @mouseover="mouseOver('item_' + item.id)"
                        :ref="'item_'+ item.id"
                    >
                        {{item.name}}
                        <span v-if="item.id == activeID" class="sr-only">(current)</span>
                    </a>
                    <a v-else class="nav-link" href="#" :id="item.id">
                        {{item.name}}
                        <span v-if="item.id == activeID" class="sr-only">(current)</span>
                    </a>
                    <MenuItem class="animate slideIn" :items="item.children" :parent="item.id"></MenuItem>
                </li>
            </ul>
        </div>
    </div>
</template>
<style>
@media (min-width: 992px) {
    .animate {
        animation-duration: 0.3s;
        -webkit-animation-duration: 0.3s;
        animation-fill-mode: both;
        -webkit-animation-fill-mode: both;
    }
}

@keyframes slideIn {
    0% {
        transform: translateY(1rem);
        opacity: 0;
    }
    100% {
        transform: translateY(0rem);
        opacity: 1;
    }
    0% {
        transform: translateY(1rem);
        opacity: 0;
    }
}

@-webkit-keyframes slideIn {
    0% {
        -webkit-transform: transform;
        -webkit-opacity: 0;
    }
    100% {
        -webkit-transform: translateY(0);
        -webkit-opacity: 1;
    }
    0% {
        -webkit-transform: translateY(1rem);
        -webkit-opacity: 0;
    }
}
.slideIn {
    -webkit-animation-name: slideIn;
    animation-name: slideIn;
}
.navbar .dropdown-toggle,
.navbar .dropdown-menu a {
    cursor: pointer;
}

.navbar .dropdown-item.active,
.navbar .dropdown-item:active {
    color: inherit;
    text-decoration: none;
    background-color: inherit;
}

body {
    background-color: #343a40;
}
.bg-dark .dropdown-menu {
    min-width: 200px;
    padding: 5px 0;
    margin: 2px 0 0;
    background-color: #343a40;
    border: 1px solid rgba(0, 0, 0, 0.7);
    border: 1px solid rgba(0, 0, 0, 0.15);
    -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
}

.bg-dark .dropdown-menu .divider {
    border: 1px solid rgba(0, 0, 0, 0.8);
}
.bg-dark .dropdown-menu > li > a {
    padding: 6px 20px;
    color: rgba(255, 255, 255, 0.8);
}
.bg-dark .dropdown-item:focus,
.bg-dark .dropdown-item:hover {
    color: rgba(255, 255, 255, 0.8);
    text-decoration: none;
    background-color: #343a40;
}
.bg-dark .dropdown-menu > li > a:hover,
.bg-dark .dropdown-menu > li > a:focus {
    color: rgba(255, 255, 255, 0.7);
    text-decoration: none;
    background-color: #343a40;
}
.bg-dark .dropdown-menu > .active > a,
.bg-dark .dropdown-menu > .active > a:hover,
.bg-dark .dropdown-menu > .active > a:focus {
    color: rgba(255, 255, 255, 0.7);
    text-decoration: none;
    background-color: #343a40;
    outline: 0;
}
@media (min-width: 767px) {
    .navbar .dropdown-toggle:not(.nav-link)::after {
        display: inline-block;
        width: 0;
        height: 0;
        margin-left: 0.5em;
        vertical-align: 0;
        border-bottom: 0.3em solid transparent;
        border-top: 0.3em solid transparent;
        border-left: 0.3em solid;
    }
}
</style>
<script>
/* eslint-disable */
$(document).ready(function() {
    $(".navbar .dropdown-item.dropdown").on("mouseover", function(e) {
        var $el = $(this).children(".dropdown-toggle");
        if ($el.length > 0 && $(e.target).hasClass("dropdown-toggle")) {
            var $parent = $el.offsetParent(".dropdown-menu");
            $(this)
                .parent("li")
                .toggleClass("open");

            if (!$parent.parent().hasClass("navbar-nav")) {
                if ($parent.hasClass("show")) {
                    $parent.removeClass("show");
                    $el.next().removeClass("show");
                    $el.next().css({ top: -999, left: -999 });
                } else {
                    $parent
                        .parent()
                        .find(".show")
                        .removeClass("show ");
                    $parent.addClass("show ");
                    $el.next().addClass("show");
                    $el.next().css({
                        top: $el[0].offsetTop,
                        left: $parent.outerWidth()
                    });
                }
                e.preventDefault();
                e.stopPropagation();
            }
            return;
        }
    });

    $(".navbar .dropdown").on("hidden.bs.dropdown", function() {
        $(this)
            .find("li.dropdown")
            .removeClass("show open ");
        $(this)
            .find("ul.dropdown-menu")
            .removeClass("show open ");
    });
});
import MenuItem from "./MenuItem.vue";

export default {
    data() {
        return {
            // Menu data like data from database
            menuData: [
                {
                    id: 1,
                    level: 1,
                    parent: 0,
                    name: "Menu A",
                    icon: "far fa-folder"
                },
                {
                    id: 2,
                    level: 1,
                    parent: 0,
                    name: "Menu B",
                    icon: "far fa-folder"
                },
                {
                    id: 3,
                    level: 1,
                    parent: 0,
                    name: "Menu C"
                },
                {
                    id: 4,
                    level: 1,
                    parent: 0,
                    name: "Menu D"
                },
                {
                    id: 5,
                    level: 2,
                    parent: 1,
                    name: "Menu A.1"
                },
                {
                    id: 6,
                    level: 2,
                    parent: 1,
                    name: "Menu A.2",
                    icon: "far fa-folder"
                },
                {
                    id: 7,
                    level: 2,
                    parent: 2,
                    name: "Menu B.1",
                    icon: "far fa-folder"
                },
                {
                    id: 8,
                    level: 2,
                    parent: 2,
                    name: "Menu B.2",
                    icon: "far fa-folder"
                },
                {
                    id: 9,
                    level: 2,
                    parent: 2,
                    name: "Menu B.3"
                },
                {
                    id: 10,
                    level: 3,
                    parent: 6,
                    name: "Menu A.2.1"
                },
                {
                    id: 11,
                    level: 3,
                    parent: 6,
                    name: "Menu A.2.2"
                },
                {
                    id: 12,
                    level: 3,
                    parent: 6,
                    name: "Menu A.2.3"
                },
                {
                    id: 13,
                    level: 3,
                    parent: 7,
                    name: "Menu B.1.2"
                },
                {
                    id: 14,
                    level: 3,
                    parent: 8,
                    name: "Menu B.2.1",
                    icon: "far fa-folder"
                },
                {
                    id: 15,
                    level: 3,
                    parent: 14,
                    name: "Menu B.2.1.1"
                },
                {
                    id: 16,
                    level: 3,
                    parent: 14,
                    name: "Menu B.2.1.2"
                }
            ],
            menus: [],
            activeID: 0
        };
    },
    components: { MenuItem },
    methods: {
        mouseOver(ref) {
            var elem = this.$refs[ref];
            elem[0].click();
        },
        loadMenu() {
            var map = {},
                node,
                roots = [],
                i;
            for (i = 0; i < this.menuData.length; i += 1) {
                map[this.menuData[i].id] = i; // initialize the map
                this.menuData[i].children = []; // initialize the children
            }
            for (i = 0; i < this.menuData.length; i += 1) {
                node = this.menuData[i];
                if (node.parent !== 0) {
                    this.menuData[map[node.parent]].children.push(node);
                } else {
                    roots.push(node);
                }
            }
            this.menus = roots;
        }
    },
    mounted() {
        // convert data menu flat to tree
        this.loadMenu();
    }
};
</script>
