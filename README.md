# vue-generic-table
A simple vue generic table inspired by this [vue example](https://vuejs.org/v2/examples/grid-component.html).

## Features
- Search
- Sortable on the columns
- Pagination
- Row limit
- Buttons to show all rows or less

## genericTable component

### Required props
- `:data` (Array) array of the object we want to display in the table
- `:columns` (Array) shown columns in the data object

### Optional props
- `:search-query` (String) initial search query
- `:init-limit` (Number) initial limit
- `:is-paginated` (Boolean) display table with pagination or not
- `:init-sort-key` (String) initial sort key on a given column from the required props


## Requirements
- NodeJS >= 6.10
- Yarn >= 1.7.0

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Lints and fixes files
```
yarn run lint
```