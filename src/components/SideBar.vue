<template>
    <div class="sidebar-header">
        <h3 class="text-size"><img :src="require('@/assets/Ministère.png')" height="40" alt="MDB Logo"
                loading="lazy" /><span>Avancement </span></h3>
    </div>
    <ul class="list-unstyled components">
        <li class="">
            <RouterLink to="/dashboard" class="text-white"> <v-icon style="top: 0;">mdi-monitor-dashboard</v-icon>
                <span>Dashboard</span>
            </RouterLink>
        </li>

        <hr class="dropdown-divider" />

        <li class="dropdown">
            <a href="#homeSubmenu1" data-toggle="collapse" aria-expanded="false" class="dropdown-toggle">
                <v-icon style="top: 0;">mdi-ansible</v-icon><span class="text-white">Avancement</span></a>
            <ul class="collapse list-unstyled menu pl-4" id="homeSubmenu1">
                <li>
                    <RouterLink to="/avancement" @click.prevent="actionAvenantTout()" style="font-size: 14px;"
                        class="text-white" aria-current="page">Liste complète</RouterLink>
                </li>
                <li>
                    <RouterLink to="/avancement" @click.prevent="actionAvenant6M()" style="font-size: 14px;"
                        class="text-white">Avancement bientôt </RouterLink>
                </li>
                <li>
                    <RouterLink to="/avancement" @click.prevent="actionAvenantTard()" style="font-size: 14px;"
                        class="text-white">Avancement en retard</RouterLink>
                </li>
            </ul>
        </li>

        <li class="dropdown">
            <a href="#pageSubmenu2" data-toggle="collapse" aria-expanded="false" class="dropdown-toggle">
                <v-icon style="top: 0;">mdi-alpha-c-box</v-icon><span class="text-white">Contractuel</span></a>
            <ul class="collapse list-unstyled menu pl-4" id="pageSubmenu2">
                <li>
                    <RouterLink to="/contractuel" @click.prevent="actionContratTout()" style="font-size: 14px;"
                        class="text-white">Liste complète</RouterLink>
                </li>
                <li>
                    <RouterLink to="/contractuel" @click.prevent="actionContrat6M()" style="font-size: 14px;"
                        class="text-white">Fin Contrat dans 6 mois</RouterLink>
                </li>
                <li>
                    <RouterLink to="/contractuel" @click.prevent="actionContratTard()" style="font-size: 14px;"
                        class="text-white">Contrat en retard</RouterLink>
                </li>
            </ul>
        </li>

        <li class="dropdown">
            <a href="#pageSubmenu3" data-toggle="collapse" aria-expanded="false" class="dropdown-toggle">
                <v-icon style="top: 0;">mdi-alpha-r-box</v-icon>
                <span class="text-white">Retraite</span></a>
            <ul class="collapse list-unstyled menu pl-4" id="pageSubmenu3">
                <li>
                    <RouterLink to="/retraite" @click.prevent="actionRetraite1A()" class="text-white">Retraiter dans 12 mois
                    </RouterLink>
                </li>
                <li>
                    <RouterLink to="/retraite" @click.prevent="actionRetraiteTard()" class="text-white">Retraite en retard
                    </RouterLink>
                </li>
            </ul>
        </li>

        <hr class="dropdown-divider" />
        <li class="" v-if="ajouter">
            <usecsv-button importerKey="53c08f3e-c394-4f41-8791-49dc252ded3a" :user="{ userId: '12345' }"
                :metadata="{ anotherId: '123' }" :onData="onData" v-slot="slotProps">
                <a href="#" class="text-white" @click="slotProps.openModal()">
                    <v-icon style="top: 0;">mdi-import</v-icon><span>Importer Data</span>
                </a>
            </usecsv-button>

        </li>
        <li class="">
            <a class="text-white"   @click.prevent="deconnecter()"><v-icon style="top: 0;">mdi-logout</v-icon><span>Se déconnecter</span></a>
        </li>
    </ul>
</template> 

<script>

import { accountService } from "@/_service";
import { mapActions } from "vuex";
import UseCSVButton from "@usecsv/vuejs3"
export default {
    name: 'HomePage',
    components: {
        "usecsv-button": UseCSVButton
    },
    data() {
        return {
            ajouter: false,
        };
    },
    mounted() {
        const user = JSON.parse(localStorage.getItem("user-info"));
        this.nomConnecter = user[0].nom + ' ' + user[0].prenom;
        if (user[0].role == 'ADMIN') {
            this.ajouter = true;
        }
    },
    
    methods: {
        ...mapActions([
            'actionAvenantTout', 'actionAvenant6M', 'actionAvenantTard',
            'actionContratTout', 'actionContrat6M', 'actionContratTard',
            'actionRetraite1A', 'actionRetraiteTard',
        ]),
        onData(results) {
            // Do something with the data here
            console.log('Rows => ', results.rows);
            // var donnee = new FormData();

            // for (let i = 0; i < results.rows.lenght; i++) {

            //     donnee.append('code', results.rows[i].col1);
            //     donnee.append('soa', results.rows[i].col2);
            //     donnee.append('libelle', results.rows[i].col3);

            //     accountService.addImport(donnee).then((res) => {
            //         if (res.data.error) {
            //             console.log("🚫error 1...!num:", i, res.data.message);
            //         } else {
            //             console.log("✅success 1...! num:", i, res.data.message);
            //         }
            //     }).catch((err) => { console.log(err) });
            // }

        },
        deconnecter() {
            localStorage.clear();
            this.$router.push({ name: 'Login' });
        },

    }

}



</script>
<style>
.text-size {
    font-size: 18px;
}

.fotsy a {
    color: white;
}</style>
