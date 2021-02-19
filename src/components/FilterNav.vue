<template>
  <nav class="filter-nav">
      <button :class="{ active: currentFilter === 'all'}" @click="updateFilter('all')">View All</button>
      <button :class="{ active: currentFilter === 'completed'}" @click="updateFilter('completed')">Completed</button>
      <button :class="{ active: currentFilter === 'ongoing'}" @click="updateFilter('ongoing')">Ongoing</button>
  </nav>
</template>

<script>
export default {
    props: ['currentFilter'],
    setup(props, { emit }) {
      const updateFilter = by => {
          emit('filterChange', by)
        }

      return { updateFilter }
    }
}
</script>

<style>
 .filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #555;
  }
</style>