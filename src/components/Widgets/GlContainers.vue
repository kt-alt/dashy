<template>
  <div>
    <input v-model='filterText' placeholder='Filter by name' />
    <table>
      <thead>
        <tr>
          <th @click=sortBy(name)>Name</th>
          <th @click=sortBy(age)>Age</th>
          <th @click=sortBy(city)>City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for='item in filteredItems' :key='item.id'>
          <td>{{ item.name }}</td>
          <td>{{ item.age }}</td>
          <td>{{ item.city }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          id: 1, name: 'John', age: 30, city: 'New York',
        },
        {
          id: 2, name: 'Alice', age: 25, city: 'Los Angeles',
        },
        {
          id: 3, name: 'Bob', age: 35, city: 'Chicago',
        },
      ],
      sortByKey: null,
      sortAsc: true,
      filterText: '',
    };
  },
  computed: {
    sortedItems() {
      const key = this.sortByKey;
      const order = this.sortAsc ? 1 : -1;

      return this.items.slice().sort((a, b) => {
        if (a[key] < b[key]) return -order;
        if (a[key] > b[key]) return order;
        return 0;
      });
    },
    filteredItems() {
      const filterText = this.filterText.toLowerCase();
      return this.sortedItems.filter((item) => item.name.toLowerCase().includes(filterText));
    },
  },
  methods: {
    sortBy(key) {
      if (this.sortByKey === key) {
        this.sortAsc = !this.sortAsc;
      } else {
        this.sortByKey = key;
        this.sortAsc = true;
      }
    },
  },
};
</script>
