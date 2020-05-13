<template>
    <div>
        <b-form>
            <b-row>
                <b-col>
                    <b-form-group
                        label="Consulta"
                        label-for="query"
                    >
                        <b-form-input
                            id="query"
                            v-model="query"
                            autocomplete="off"
                        >
                        </b-form-input>
                    </b-form-group>
                </b-col>
                <b-col>
                    <b-form-group
                        label="Desde"
                        label-for="from"
                    >
                        <datepicker
                            v-model="from"
                            id="from"
                            name="from"
                            :minimumView="'year'"
                            :maximumView="'year'"
                            :initialView="'year'"
                            :language="languages[lang]"
                            :format="'yyyy'"
                            :bootstrap-styling="true"
                        ></datepicker>
                    </b-form-group>
                </b-col>
                <b-col>
                    <b-form-group
                        label="Hasta"
                        label-for="to"
                    >
                        <datepicker
                            v-model="to"
                            id="to"
                            name="to"
                            :minimumView="'year'"
                            :maximumView="'year'"
                            :initialView="'year'"
                            :language="languages[lang]"
                            :format="'yyyy'"
                            :bootstrap-styling="true"
                        ></datepicker>
                    </b-form-group>
                </b-col>
            </b-row>
            
            <b-row>
                <b-col>
                    <b-form-group
                        label="Precio mínimo"
                        label-for="min_price"
                    >
                        <b-form-input
                            id="min_price"
                            v-model="min_price"
                            type="number"
                            :step="1000"
                        >
                        </b-form-input>
                    </b-form-group>
                </b-col>
                <b-col>
                    <b-form-group
                        label="Precio máximo"
                        label-for="max_price"
                    >
                        <b-form-input
                            id="max_price"
                            v-model="max_price"
                            type="number"
                            :step="1000"
                        >
                        </b-form-input>
                    </b-form-group>
                </b-col>
                <b-col>
                    <b-form-group
                        label="¿Disponible?"
                        label-for="available"
                    >
                        <b-form-select
                            id="available"
                            :options="options"
                            v-model="available"
                        >
                        </b-form-select>
                    </b-form-group>
                </b-col>
            </b-row>

            <b-row>
                <b-col>
                    <b-button
                        @click.prevent="resetFilter"
                        variant="danger"
                    >
                        Restablecer filtros
                    </b-button>
                </b-col>
            </b-row>

        </b-form>
    </div>
</template>

<script>
  import Datepicker from 'vuejs-datepicker';
  import * as langs from "vuejs-datepicker/src/locale";

  export default {
    components: {
      Datepicker
    },
    data () {
      return {
        options: [
          { text: 'Sí', value: true },
          { text: 'No', value: false },
        ],
        languages: langs,
        lang: 'es'
      }
    },
    computed: {
      query: {
        get () {
          return this.$store.state.filter.query
        },
        set (value) {
          this.$store.commit('setFilter', {
            filter: 'query',
            value
          })
        }
      },
      from: {
        get () {
            return new Date(this.$store.state.filter.from, 1, 1)
        },
        set (value) {
          this.$store.commit('setFilter', {
            filter: 'from',
            value: new Date(value).getFullYear()
          })
        }
      },
      to: {
        get () {
          return new Date(this.$store.state.filter.to, 1, 1)
        },
        set (value) {
          this.$store.commit('setFilter', {
            filter: 'to',
            value: new Date(value).getFullYear()
          })
        }
      },
      min_price: {
        get () {
          return this.$store.state.filter.min_price
        },
        set (value) {
          this.$store.commit('setFilter', {
            filter: 'min_price',
            value: parseFloat(value)
          })
        }
      },
      max_price: {
        get () {
          return this.$store.state.filter.max_price
        },
        set (value) {
          this.$store.commit('setFilter', {
            filter: 'max_price',
            value: parseFloat(value)
          })
        }
      },
      available: {
        get () {
          return this.$store.state.filter.available
        },
        set (value) {
          this.$store.commit('setFilter', {
            filter: 'available',
            value
          })
        }
      },
    },
    methods: {
      resetFilter () {
        this.$store.commit('resetFilter')
      }
    }
  }
</script>