
<template>
    <div>
        <!--  Bfrtip -->
        <div class="mr-4 ml-4 mt-3 mb-3">
            <div class=" table-responsive">
                <DataTable :data="getContrat" :columns="columns"
                    class="table table-hover table-striped table-bordered display" :options="{
                        responsive: false, autoWidth: false, dom: 'Blrftip', language: {
                            search: 'Recherche', zeroRecords: 'aucune donnée disponible',
                            info: 'Affichage de _START_ à _END_ sur _TOTAL_ entrées',
                            infoFiltered: '(Montrer _MAX_ entrées)',
                            paginate: { first: 'Prémière', previous: 'Précédent', next: 'Suivant', last: 'Dernière' }
                        }, buttons: botones,

                    }">
                    <thead class="table-success ">
                        <tr class="toto">
                            <th class="fw-bolder" style="font-size: 14px;">ID</th>
                            <th class="fw-bolder" style="font-size: 14px;">MATRICULE</th>
                            <th class="fw-bolder" style="font-size: 14px;">NOMS</th>
                            <th class="fw-bolder" style="font-size: 14px;">STATUT</th>
                            <th class="fw-bolder" style="font-size: 14px;">CORPS CODE</th>
                            <th class="fw-bolder" style="font-size: 14px;">FIN DU CONTRAT</th>
                            <th class="fw-bolder" style="font-size: 14px;">SECTION CODE</th>
                            <th class="fw-bolder" style="font-size: 14px;">SOA CODE</th>
                            <th class="fw-bolder" style="font-size: 14px;">SOA LIBELLE</th>
                        </tr>
                    </thead>
                </DataTable>
            </div>
        </div>

    </div>
</template>
  
<script>

import DataTable from 'datatables.net-vue3';
import DataTableLib from 'datatables.net-bs5';
import Buttons from 'datatables.net-buttons-bs5';
import ButtonsHtml5 from 'datatables.net-buttons/js/buttons.html5';
import Print from 'datatables.net-buttons/js/buttons.print';
import pdfmake from 'pdfmake';
import pdfFonts from 'pdfmake/build/vfs_fonts';
pdfmake.vfs = pdfFonts.pdfMake.vfs;
import 'datatables.net-responsive-bs5';
import JsZip from 'jszip';

window.JSZip = JsZip;
DataTable.use(DataTableLib);
DataTable.use(pdfmake);
DataTable.use(ButtonsHtml5);

import { ref, computed } from "vue";
import { useStore } from "vuex";
export default {
    components: {
        DataTable
    },
    data() {
        return {

            dataAgents: null,
            scrollX: true,
            columns: [
                { data: 'ID' },
                { data: 'AGENT_MATRICULE' },
                { data: 'NOMS' },
                { data: 'STATUT' },
                { data: 'CORPS_CODE' },
                { data: 'FIN_CONTRAT' },
                { data: 'SECTION_CODE' },
                { data: 'SOA' },
                { data: 'REG_CODE' },
            ],
            botones: [
                {
                    title: 'Liste des tout agents',
                    extend: 'excelHtml5',
                    text: '<strong>Excel</strong>',
                    className: 'btn btn-success'
                },
                {
                    title: 'Liste des tout agents',
                    extend: 'print',
                    text: '<strong>Imprimer</strong>',
                    className: 'btn btn-danger'
                },
                {
                    title: 'Liste des tout agents',
                    extend: 'copy',
                    text: ' <strong>Copie</strong>',
                    className: 'btn btn-dark'
                },
            ],
        };
    },
    // computed:{
    //     ...mapGetters(['getContrat']),
    // },
    async setup() {
        const store = useStore();
        const getContrat =  computed(() => store.getters.getContrat);
        const getTitre = computed(() => store.getters.getTitre)
        await new Promise(getContrat => setTimeout(getContrat, 4000))
        return { getContrat, getTitre }
    }

};
</script>


<style>
.fw-bolder {
    font-size: 14px;
}

.dataTables_wrapper .dataTables_filter input {
    font-size: 14px;
    width: 300px;
}

.dataTables_filter {
    position: absolute;
    right: 40px;
    top: 70px;
    display: flex;
    justify-content: flex-end;
}

.odd td,
.even td {
    font-size: 14px;
}
</style>
  