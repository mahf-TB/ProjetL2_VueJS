<template>
    <div class="card mt-0  p-3">
        <div class="row g-5">
            <div class="col-md-6">
                <h4 class="toUpper">{{ getTitre }}</h4>
            </div>
            <div class="col-md-6">
                <div class="xp-searchbar">
                    <form>
                        <div class="input-group" style="width:100%;">
                            <input type="date" class="form-control" placeholder="Date Debut">
                            <input type="date" class="form-control" placeholder="Date Fin">
                            <div class="input-group-append">
                                <button class="btn" type="submit" id="button-addon2">RECHERCHE</button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
    <Suspense >
        <template #default>
            <div class="container-fluid">
                <div class="card p-3">
                    <DatatableRetraite />
                </div>
            </div>
        </template>
        <template #fallback>
            <div class="container-fluid">
                chargement...
            </div>
        </template>
    </Suspense>
</template>
 
<script>

import { mapGetters } from "vuex";
import sousHeader from "@/components/sousHeader.vue";
import DatatableRetraite from '@/views/datatables/DatatableRetraite.vue';
export default {
    name: 'Retraite',
    components: {
        DatatableRetraite, sousHeader
    },
    computed: {
        ...mapGetters(['getTitre']),
    },
}
</script>