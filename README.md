# Vue-3 Pagination

Simple pagination component for vue-3

- [Dependencies](#dependencies)
- [Installation](#installation)
  - [NPM](#npm)
- [Usage](#usage)
- [Api](#api)
  - [Props](#props)
  - [Events](#events)
- [Development](#development)

# Dependencies

- Vue.js (3.2.37). Required.

# Installation

## NPM

    npm install vue-3-pagination

import the script:

    import { v3Paginate } from "@ahm-zobyer/vue-3-pagination";

import the css:

    import "@ahm-zobyer/vue-3-pagination/dist/style.css";

# Usage

Register the component :

```js
components: {
  v3Paginate;
}
```

```vue
<v3Paginate :totalElement="100" :elementPerPage="10" @onPageClick="getData" />
```

# Api

## Props

| Name             | Type   | Description                                                     |
| ---------------- | ------ | --------------------------------------------------------------- |
| `totalElement`   | Number | (optional) defines total no of data present.                    |
| `elementPerPage` | Number | (optional) defines number data which will be shown on per page. |

### Events

| Name          | Description                                                                     |
| ------------- | ------------------------------------------------------------------------------- |
| `onPageClick` | Triggered when a user changes page. Passes the new `page` index as a parameter. |

# Development

To work on the library locally, run the following command:

install dependencies

```bash
npm i
```

run on local machine

```bash
npm run dev
```
