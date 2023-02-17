<template>
  <div class="py-4 container-fluid">
    <div class="row">
      <div class="col-12">
        <v-data-table :columns="columns" :data="dataSet" :isShowPerPageOption="perPageOptions" :isSearchAble="search"
                      :pagination="pagination" :csvDownload="csvDownload" filterClass="col-md-5" searchClass="col-md-4">
          <template #header>
            <div class="row">
              <div class="col-md-9">
                <div class="d-flex align-items-center justify-content-between">
                  <h6>The header of the list</h6>
                  <button type="button" class="mb-0 btn btn-outline-primary btn-sm" @click="">Create data</button>
                </div>
              </div>
              <div class="col-md-3">
                  <div class="form-check form-switch d-flex justify-content-center align-items-center">
                    <input class="form-check-input me-2" type="checkbox" role="switch" id="flexSwitchCheckChecked"
                           v-model="openFilter">
                    <label class="form-check-label" for="flexSwitchCheckChecked">Show filter option</label>
                  </div>
              </div>
            </div>
          </template>
          <template #filters v-if="openFilter">
            <div class="dropdown" :class="{'show': isFocused }" style="position: absolute">
              <button class="btn btn-primary dropdown-toggle" type="button" id="dropdownMenuButton"
                      data-mdb-toggle="dropdown" :aria-expanded="isFocused" @click="isFocused = !isFocused">
                Checkbox dropdown
              </button>
              <ul class="dropdown-menu" :class="{'show': isFocused }" aria-labelledby="dropdownMenuButton"
                  style="position: relative;" @click="isFocused = false">
                <li>
                  <a class="dropdown-item" href="#">
                    <div class="form-check">
                      <input class="form-check-input" type="checkbox" v-model="perPageOptions" id="Checkme1"/>
                      <label class="form-check-label" for="Checkme1">Hide Per Page </label>
                    </div>
                  </a>
                </li>
                <li>
                  <a class="dropdown-item" href="#">
                    <div class="form-check">
                      <input class="form-check-input" type="checkbox" v-model="search" id="Checkme2" checked/>
                      <label class="form-check-label" for="Checkme2">Hide Search Input</label>
                    </div>
                  </a>
                </li>
                <li>
                  <a class="dropdown-item" href="#">
                    <div class="form-check">
                      <input class="form-check-input" type="checkbox" v-model="pagination" id="Checkme3"/>
                      <label class="form-check-label" for="Checkme3">Hide Pagination</label>
                    </div>
                  </a>
                </li>
                <li>
                  <a class="dropdown-item" href="#">
                    <div class="form-check">
                      <input class="form-check-input" type="checkbox" v-model="csvDownload" id="Checkme4" checked/>
                      <label class="form-check-label" for="Checkme4">Hide CSV Download Button</label>
                    </div>
                  </a>
                </li>
              </ul>
            </div>
          </template>

          <template #table_data="{item, index}">
            <td>
              <span class="text-secondary text-xs font-weight-bold ps-3">{{ index }}</span>
            </td>
            <td>
              <span class="text-secondary text-xs font-weight-bold ps-3">{{ item.title }}</span>
            </td>
            <td>
              <span class="text-secondary text-xs font-weight-bold ps-3 show-dot-sign">{{ item.body }}</span>
            </td>
            <td>
              <span>
                  <a
                      href="javascript:;"
                      class="text-secondary text-xs font-weight-bold ps-3"
                  >Edit</a>
                  <a
                      href="javascript:;"
                      class="text-danger text-xs font-weight-bold ps-3"
                  >Delete</a>
              </span>
            </td>
          </template>
        </v-data-table>
      </div>
    </div>
  </div>
</template>

<script>
import {VDataTable} from "v-datatable"

export default {
  components: {VDataTable},
  data() {
    return {
      dataSet: [],
      columns: [
        {title: "SL", sort_key: ''},
        {title: "Name", sort_key: 'title'},
        {title: "Description", sort_key: 'body'},
        {title: "Action", sort: ''}
      ],
      openFilter: false,
      pagination: true,
      perPageOptions: true,
      search: true,
      csvDownload: true,

      isFocused: false
    }
  },
  mounted() {
    setTimeout(() => {
      fetch('https://jsonplaceholder.typicode.com/posts')
          .then(response => response.json())
          .then(json => {
            this.dataSet = json;
          })
    }, 1)
  }
};
</script>

<style>
@import "v-datatable/dist/style.css";
</style>

