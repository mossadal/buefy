<template>
    <div id="app">
        <vue-progress-bar></vue-progress-bar>

        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name: 'Buefy',
        created() {
            this.$Progress.start()
            this.$router.beforeEach((to, from, next) => {
                this.$Progress.start()
                next()
            })
            this.$router.afterEach((to, from) => {
                this.$Progress.finish()
            })
        },
        mounted() {
            this.$Progress.finish()
        }
    }
</script>

<style lang="scss">
    @import "./assets/scss/main.scss";

    // Helpers

    .example {
        border: 1px solid $warning;
        border-top-right-radius: $radius;
        color: rgba(0, 0, 0, 0.7);
        padding: 1.5rem;
        position: relative;
        &:not(:first-child) {
            margin-top: 2rem;
        }
        &:not(:last-child) {
            margin-bottom: 1.5rem
        }
        &:before {
            background: $warning;
            border-radius: $radius $radius 0 0;
            bottom: 100%;
            content: "Example";
            display: inline-block;
            font-size: 7px;
            font-weight: bold;
            left: -1px;
            letter-spacing: 1px;
            padding: 3px 5px;
            position: absolute;
            text-transform: uppercase;
            vertical-align: top;
        }
        + .example-code {
            border: 1px solid $warning;
            border-top: none;
            margin-top: -1.5rem;
            &:not(:last-child) {
                margin-bottom: 1.5rem
            }
            + .example-code {
                border: 1px solid $warning;
                border-top: none;
                margin-top: -1.5rem;
                &:not(:last-child) {
                    margin-bottom: 1.5rem
                }
            }
        }
        &.is-flex {
            align-items: center;
        }
    }

    // Generic

    pre {
        @include tablet {
            white-space: pre-wrap;
        }
        code {
            max-height: 400px;
            &.hljs {
                background: inherit;
                color: inherit;
                padding: 1.25rem 1.5rem;
            }
        }
    }

    ::selection {
        background: lighten($primary, 5%);
        color: $primary-invert;
    }

    // Home

    .home {
        .logo-rounded,
        .subtitle,
        .npm,
        .github-button {
            margin-bottom: 1.5rem;
        }
        .buttons {
            margin-bottom: 0.5rem;
        }
        .logo-rounded {
            background: $light;
            display: inline-block;
            padding: 2.5rem;
            border-radius: 32px;
            box-shadow: 0 20px 60px rgba(10, 10, 10, 0.05), 0 5px 10px rgba(10, 10, 10, 0.1), 0 1px 1px rgba(10, 10, 10, 0.2);
            img {
                width: 320px;
            }
            @include mobile {
                padding: 2rem;
                img {
                    width: 220px;
                }
            }
        }
        .button + .button {
            margin-left: 0.5rem;
        }
        .npm {
            display: inline-flex;
            font-size: 1.1em;
            color: lighten($primary, 20%);
            background: darken($primary, 20%);
        }
    }

    // Temporary fix for https://github.com/jgthms/bulma/issues/837
    .hero.is-primary .hero-head .navbar {
        background: $primary;
        color: $primary-invert;
        box-shadow: 0 1px 0 rgba($primary-invert, 0.2);
        .has-dropdown .navbar-link:after {
            border-color: $primary-invert;
        }
        a.navbar-item {
            background: transparent;
        }
        a.navbar-link {
            background: transparent;
            color: rgba($primary-invert, 0.7);
            &.is-active,
            &:hover {
                color: $primary-invert;
            }
        }
        .navbar-burger {
            background: transparent;
            span {
                background: $primary-invert;
            }
            &:hover {
                background: darken($primary, 2.5%);
            }
        }
        @include touch {
            .has-dropdown .navbar-item {
                &:not(.is-active) {
                    color: rgba($primary-invert, 0.7) !important;
                }
                &:hover {
                    color: $primary-invert !important;
                }
            }
        }
    }
</style>
