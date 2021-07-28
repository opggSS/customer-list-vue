<template>
  <div class="container">
    <div>
      Sort By
      <select name="sortBy" id="sortBy" value="" @change="handleSort">
        <option value="">default</option>
        <option value="firstName">First Name</option>
        <option value="lastName">last Name</option>
        <option value="email">email</option>
        <option value="address">address</option>
        <option value="phone">Phone</option>
      </select>
    </div>
    <div>
      Filter
      <select name="filter" id="filter" @change="handleFilter">
        <option value="default">default</option>
        <option value="hasAddress">has Address</option>
      </select>
    </div>
    <div>
      <input
        type="text"
        name="search"
        @input="handleSearch"
        placeholder="Enter the keyword to search in first name and last name"
      />
    </div>
    <UserCard :users="updatedUsers"></UserCard>
  </div>
</template>

<script>
import UserCard from "./components/UserCard";

const sortBy = (arr, name) => {
  return arr.sort((a, b) => {
    return a[name] > b[name] ? 1 : -1;
  });
};
const applyFilter = (arr, hasEmail) => {
  return arr.filter((e) => {
    if (hasEmail) return e.address;
    return !e.address;
  });
};

const applySearch = (arr, keyword) => {
  if (keyword)
    return arr.filter((e) => {
      return (
        e.firstName.toLowerCase().includes(keyword.toLowerCase()) ||
        e.firstName.toLowerCase().includes(keyword.toLowerCase())
      );
    });
  return arr;
};

export default {
  name: "App",
  components: {
    UserCard,
  },
  methods: {
    handleSearch(e) {
      const keyword = e.target.value;
      this.currentKeyword = keyword;
      if (keyword) {
        this.updatedUsers = applySearch(
          applyFilter(
            sortBy(this.users, this.currentSortBy),
            this.currentFilter
          ),
          this.currentKeyword
        );
      } else {
        this.updatedUsers = applyFilter(
          sortBy(this.users, this.currentSortBy),
          this.currentFilter
        );
      }
      applySearch();
    },
    handleSort(e) {
      const name = e.target.value;
      this.currentSortBy = name;
      if (name === "default") {
        this.updatedUsers = applySearch(
          applyFilter(this.users, this.currentFilter),
          this.currentKeyword
        );
      } else {
        this.updatedUsers = applySearch(
          applyFilter(sortBy(this.users, name), this.currentFilter),
          this.currentKeyword
        );
      }
    },
    handleFilter(e) {
      const name = e.target.value;
      this.currentFilter = name;
      if (name === "default") {
        this.updatedUsers = applySearch(
          sortBy(this.users, this.currentSortBy),
          this.currentKeyword
        );
      } else {
        this.updatedUsers = applySearch(
          applyFilter(
            sortBy(this.users, this.currentSortBy),
            this.currentFilter
          ),
          this.currentKeyword
        );
      }
    },
  },
  mounted() {
    this.updatedUsers = this.users;
  },
  data() {
    return {
      currentKeyword: "",
      currentSortBy: "default",
      currentFilter: "default",
      updatedUsers: [],
      users: [
        {
          firstName: "aaaaaaaaaaaaaaa",
          lastName: "a",
          email: "a@a.com",
          phone: "7787887871",
          address: "3123 test St",
        },
        {
          firstName: "ccccccccccccccccccaaaaa",
          lastName: "c",
          email: "b@a.com",
          phone: "77878878782",
          address: "1123 test St",
        },
        {
          firstName: "bbbbbbbbbbbbbbbbbbbbbbb",
          lastName: "b",
          email: "c@a.com",
          phone: "7787887873",
          address: "2123 test St",
        },
        {
          firstName: "ddddddddddddd",
          lastName: "ddddddd",
          email: "dddddddd@a.com",
          phone: "7787887823",
          address: undefined,
        },
      ],
    };
  },
};
</script>

<style>
</style>
