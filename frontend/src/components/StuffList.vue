<template>
  <table>
    <thead>

      <th>Name</th>
      <th>Quantity</th>
      <th>State</th>
      <th>Actions</th>

    </thead>

    <tbody>

      <tr v-for="(stuff, i) in stuffs" v-bind:key="stuff.id">
        <td>
          {{ stuff.name }}
        </td>

        <td>
          {{ stuff.quantity }}
        </td>

        <td>
          {{ stuff.state }}
        </td>

        <td>
          <div>
            <span v-on:click="deleteStuff(stuff.id, i)">
              &#128163;
            </span>
            <span>
              <router-link v-bind:to="{ name: 'Movements', params: { id: stuff.id }}">&#128184;</router-link>
            </span>
            <span v-on:click="selectStuff(i)">
              &#128204;
            </span>
          </div>
        </td>
      </tr>

    </tbody>
  </table>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import { CreateStuff } from '@/types/Stuff'

@Component
export default class StuffList extends Vue {
  @Prop() private stuffs!: CreateStuff[]

  selectStuff (index: number): void {
    this.$emit('select-stuff', { stuff: this.stuffs[index], index })
  }

  deleteStuff (id: number, index: number): void {
    this.$emit('delete-stuff', { id, index })
  }
}
</script>

<style scoped lang="scss">
* {
  box-sizing: border-box;
}

a {
  text-decoration: none;
}

table {
  width: 100%;
  height: auto;
  border-spacing: 0;
}

thead {
  background-color: black;
  color: white;
}

th {
  padding-top: 5px;
  padding-bottom: 5px;
}

td {
  height: 35px;
}

tr td {
  border: 1px solid white;
}

tr:hover td {
  color: #42b983;
  border-top: 1px solid #42b983;
  border-bottom: 1px solid #42b983;
}
</style>
