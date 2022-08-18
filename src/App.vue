<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

import {ColumnDef, createColumnHelper, getCoreRowModel, useVueTable, FlexRender} from "@tanstack/vue-table";
import {ref} from "vue";

type Person = {
  firstName: string
  lastName: string
  age: number
  visits: number
  status: string
  progress: number
}

const defaultData: Person[] = [
  {
    firstName: 'tanner',
    lastName: 'linsley',
    age: 24,
    visits: 100,
    status: 'In Relationship',
    progress: 50,
  },
  {
    firstName: 'tandy',
    lastName: 'miller',
    age: 40,
    visits: 40,
    status: 'Single',
    progress: 80,
  },
  {
    firstName: 'joe',
    lastName: 'dirte',
    age: 45,
    visits: 20,
    status: 'Complicated',
    progress: 10,
  },
]

const columnHelper = createColumnHelper<Person>()

const columns = [
  columnHelper.accessor('firstName', {
    header: () => 'Mon super firstname',
    cell: info => info.getValue() + 'toto',
  }),
  columnHelper.accessor('visits', {
    header: () => 'Visits',
    cell: info => '<code>' + info + '</code>',
  }),
  columnHelper.accessor('status', {
    header: 'Status',
  }),
  columnHelper.accessor('progress', {
    header: 'Profile Progress',
  }),
]

const data = ref(defaultData)

const rerender = () => {
  data.value = defaultData
}

const table = useVueTable({
  get data() {
    return data.value
  },
  columns,
  getCoreRowModel: getCoreRowModel(),
})


</script>

<template>
  <div class="p-2">
    <table>
      <thead>
      <tr
          v-for="headerGroup in table.getHeaderGroups()"
          :key="headerGroup.id"
      >
        <th
            v-for="header in headerGroup.headers"
            :key="header.id"
            :colSpan="header.colSpan"
        >
          <FlexRender
              v-if="!header.isPlaceholder"
              :render="header.column.columnDef.header"
              :props="header.getContext()"
          />

        </th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="row in table.getRowModel().rows" :key="row.id">
        <td v-for="cell in row.getVisibleCells()" :key="cell.id">
<!--          <div v-if="cell.column.id === cell.column.id">
            <p>{{cell.column}}</p>
            <p>{{cell}}</p>
            <p>toto: {{cell.getValue()}}</p>
          </div>-->
          <FlexRender
              :render="cell.column.columnDef.cell"
              :props="cell.getContext()"
          />
        </td>
      </tr>
      </tbody>
      <tfoot>
      <tr
          v-for="footerGroup in table.getFooterGroups()"
          :key="footerGroup.id"
      >
        <th
            v-for="header in footerGroup.headers"
            :key="header.id"
            :colSpan="header.colSpan"
        >
          <FlexRender
              v-if="!header.isPlaceholder"
              :render="header.column.columnDef.footer"
              :props="header.getContext()"
          />
        </th>
      </tr>
      </tfoot>
    </table>
    <div class="h-4" />
    <button @click="rerender" class="border p-2">Rerender</button>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
