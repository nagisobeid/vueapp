<template>
<div>
   <section>
    <base-card>
    <h2>{{fullName}}</h2>
    <h3>${{rate}}</h3>
    </base-card>
   </section>
   <section>
    <header>
    <base-card>
        <h2>Interested? reach out</h2>
        <base-button link :to="contactLink">Contact</base-button>
        <router-view></router-view>
    </base-card>
    </header>
   </section>
   <section>
    <base-card>
    <base-badge v-for="area in areas" :key="area" :type="area" :title="area"></base-badge>
    <p>{{description}}</p>
    </base-card>
   </section>
</div>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            selectedCoach: null,
        }
    },
    computed: {
        fullName() {
            return this.selectedCoach.firstName + ' ' + this.selectedCoach.lastName
        },
        areas() {
            return this.selectedCoach.areas;
        },
        rate() {
            return this.selectedCoach.hourlyRate;
        },
        description() {
            return this.selectedCoach.description
        },
        contactLink() {
            //return this.$route.path + '/contact'
            return this.$route.path + '/' + this.id + '/contact';
            //return this.$route.path + '/' + this.id + '/contactcoach'
        }
    },
    created() {
        this.selectedCoach = this.$store.getters['coaches/coaches'].find(coach => coach.id === this.id)
    }
}
</script>