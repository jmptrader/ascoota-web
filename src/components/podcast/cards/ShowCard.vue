<style>
div.show-card-wrapper {
    margin: 10px;
}
</style>
<template>
    <div class="show-card-wrapper clickable"
         @click="goToShow">
        <md-card>
            <md-card-media>
                <img style="width: 250px;height: auto;"
                     alt="radio.name"
                     :src="show.logo_url">
            </md-card-media>
            <md-card-header>
                <div class="md-title">{{show.name}}</div>
            </md-card-header>
            <md-card-actions v-if="$store.state.isLoggedIn">
                <md-button @click.native="addToFavourites(show.id)"
                           class="md-icon-button">
                    <md-icon v-if="!inFavourites(show.id)">favorite_border</md-icon>
                    <md-icon v-else>favorite</md-icon>
                </md-button>
            </md-card-actions>
        </md-card>
    </div>
</template>
<script>
import UserService from '../../../services/ascoota/UserService';
import FlagIcon from '../../common/FlagIcon';

const service = new UserService();

export default {
    name: "showCard",
    components: {
        FlagIcon
    },
    props: {
        show: Object
    },
    methods: {
        inFavourites(showId){
            return false;
        },
        goToShow() {
            this.$router.push({ name: 'show', params: { slug: this.show.slug } });
        },
        addToFavourites(showId) {
            service.addToFavourites({
                show_id: showId
            });
        }
    }
}

</script>