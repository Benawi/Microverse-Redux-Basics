<a name="readme-top"></a>
![image](https://github.com/Benawi/Microverse-Redux-Basics/assets/21217148/2745e831-5f08-4b74-a70f-c0e7115835af)




# 📗 Table of Contents

- [📖 About the Project](#about-project)
  - [🛠 Built With](#built-with)
    - [Tech Stack](#tech-stack)
    - [Key Features](#key-features)
    - [Live Demo](#live-demo)
    <!-- - [Walkthrough](#Walkthrough) -->
- [💻 Getting Started](#getting-started)
  - [Setup](#setup)
  - [Prerequisites](#prerequisites)
  - [Install](#install)
  - [Usage](#usage)
  - [Run tests](#run-tests)
  - [Deployment](#triangular_flag_on_post-deployment)
- [👥 Authors](#authors)
- [🔭 Future Features](#future-features)
- [🤝 Contributing](#contributing)
- [⭐️ Show your support](#support)
- [🙏 Acknowledgements](#acknowledgements)

- [📝 License](#license)

# 📖 Book Store React Project <a name="about-project"></a>

Book Store React Project - Microverse! - An online Bookstore app built with React, Redux, CSS, and HTML. Users can browse books by category, add them to a cart, and proceed to checkout. The app features a search function, allowing users to search for books by title or author. project is a repository consisting of the following files:
- Html files
- CSS files
- JS files
- Html,CSS and JS linters file

## 🛠 Built With <a name="built-with"></a>

## Tech Stack <a name="tech-stack"></a>

<ul>
  <ul>
  <li><a href="https://microverse.notion.site/HTML-CSS-Get-a-head-start-275eb85fd34b4416aa06ec635d69cdaf">HTML</a></li>
  <li><a href="https://microverse.notion.site/HTML-CSS-Get-a-head-start-275eb85fd34b4416aa06ec635d69cdaf">CSS</a></li>
      <li><a href="https://microverse.notion.site/HTML-CSS-Get-a-head-start-275eb85fd34b4416aa06ec635d69cdaf">JS</a></li>
      <li><a href="https://react.dev/learn/start-a-new-react-project#create-react-app">React</a></li>
</ul>


## 🔑 Key Features <a name="key-features"></a>

# Redux Toolkit

#### React Course

[My React Course](https://www.udemy.com/course/react-tutorial-and-projects-course/?referralCode=FEE6A921AF07E2563CEF)

#### Support

Find the App Useful? [You can always buy me a coffee](https://www.buymeacoffee.com/johnsmilga)

#### Docs

[Redux Toolkit Docs](https://redux-toolkit.js.org/introduction/getting-started)

#### Install Template

```sh
npx create-react-app my-app --template redux
```

- @latest

```sh
npx create-react-app@latest my-app --template redux
```

#### Existing App

```sh
npm install @reduxjs/toolkit react-redux
```

#### @reduxjs/toolkit

consists of few libraries

- redux (core library, state management)
- immer (allows to mutate state)
- redux-thunk (handles async actions)
- reselect (simplifies reducer functions)

#### Extras

- redux devtools
- combine reducers

#### react-redux

connects our app to redux

#### Setup Store

- create store.js

```js
import { configureStore } from '@reduxjs/toolkit';

export const store = configureStore({
  reducer: {},
});
```

#### Setup Provider

- index.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
// import store and provider
import { store } from './store';
import { Provider } from 'react-redux';

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```

#### Setup Cart Slice

- application feature
- create features folder/cart
- create cartSlice.js

```js
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  cartItems: [],
  amount: 0,
  total: 0,
  isLoading: true,
};

const cartSlice = createSlice({
  name: 'cart',
  initialState,
});

console.log(cartSlice);

export default cartSlice.reducer;
```

- store.js

```js
import { configureStore } from '@reduxjs/toolkit';
import cartReducer from './features/cart/cartSlice';

export const store = configureStore({
  reducer: {
    cart: cartReducer,
  },
});
```

#### Redux DevTools

- extension

#### Access store value

- create components/Navbar.js

```js
import { CartIcon } from '../icons';
import { useSelector } from 'react-redux';

const Navbar = () => {
  const { amount } = useSelector((state) => state.cart);

  return (
    <nav>
      <div className='nav-center'>
        <h3>redux toolkit</h3>
        <div className='nav-container'>
          <CartIcon />
          <div className='amount-container'>
            <p className='total-amount'>{amount}</p>
          </div>
        </div>
      </div>
    </nav>
  );
};
export default Navbar;
```

#### Hero Icons

- [Hero Icons](https://heroicons.com/)

```css
nav svg {
  width: 40px;
  color: var(--clr-white);
}
```

#### Setup Cart

- cartSlice.js

```js
import cartItems from '../../cartItems';

const initialState = {
  cartItems: cartItems,
  amount: 0,
  total: 0,
  isLoading: true,
};
```

- create CartContainer.js and CartItem.js
- CartContainer.js

```js
import React from 'react';
import CartItem from './CartItem';
import { useSelector } from 'react-redux';

const CartContainer = () => {
  const { cartItems, total, amount } = useSelector((state) => state.cart);

  if (amount < 1) {
    return (
      <section className='cart'>
        {/* cart header */}
        <header>
          <h2>your bag</h2>
          <h4 className='empty-cart'>is currently empty</h4>
        </header>
      </section>
    );
  }
  return (
    <section className='cart'>
      {/* cart header */}
      <header>
        <h2>your bag</h2>
      </header>
      {/* cart items */}
      <div>
        {cartItems.map((item) => {
          return <CartItem key={item.id} {...item} />;
        })}
      </div>
      {/* cart footer */}
      <footer>
        <hr />
        <div className='cart-total'>
          <h4>
            total <span>${total}</span>
          </h4>
        </div>
        <button className='btn clear-btn'>clear cart</button>
      </footer>
    </section>
  );
};

export default CartContainer;
```

- CartItem.js

```js
import React from 'react';
import { ChevronDown, ChevronUp } from '../icons';

const CartItem = ({ id, img, title, price, amount }) => {
  return (
    <article className='cart-item'>
      <img src={img} alt={title} />
      <div>
        <h4>{title}</h4>
        <h4 className='item-price'>${price}</h4>
        {/* remove button */}
        <button className='remove-btn'>remove</button>
      </div>
      <div>
        {/* increase amount */}
        <button className='amount-btn'>
          <ChevronUp />
        </button>
        {/* amount */}
        <p className='amount'>{amount}</p>
        {/* decrease amount */}
        <button className='amount-btn'>
          <ChevronDown />
        </button>
      </div>
    </article>
  );
};

export default CartItem;
```

#### First Reducer

- cartSlice.js
- Immer library

```js
const cartSlice = createSlice({
  name: 'cart',
  initialState,
  reducers: {
    clearCart: (state) => {
      state.cartItems = [];
    },
  },
});

export const { clearCart } = cartSlice.actions;
```

- create action

```js
const ACTION_TYPE = 'ACTION_TYPE';

const actionCreator = (payload) => {
  return { type: ACTION_TYPE, payload: payload };
};
```

- CartContainer.js

```js
import React from 'react';
import CartItem from './CartItem';
import { useDispatch, useSelector } from 'react-redux';

const CartContainer = () => {
  const dispatch = useDispatch();

  return (
    <button
      className='btn clear-btn'
      onClick={() => {
        dispatch(clearCart());
      }}
    >
      clear cart
    </button>
  );
};

export default CartContainer;
```

#### Remove, Increase, Decrease

- cartSlice.js

```js
import { createSlice } from '@reduxjs/toolkit';
import cartItems from '../../cartItems';

const initialState = {
  cartItems: [],
  amount: 0,
  total: 0,
  isLoading: true,
};

const cartSlice = createSlice({
  name: 'cart',
  initialState,
  reducers: {
    clearCart: (state) => {
      state.cartItems = [];
    },
    removeItem: (state, action) => {
      const itemId = action.payload;
      state.cartItems = state.cartItems.filter((item) => item.id !== itemId);
    },
    increase: (state, { payload }) => {
      const cartItem = state.cartItems.find((item) => item.id === payload.id);
      cartItem.amount = cartItem.amount + 1;
    },
    decrease: (state, { payload }) => {
      const cartItem = state.cartItems.find((item) => item.id === payload.id);
      cartItem.amount = cartItem.amount - 1;
    },
    calculateTotals: (state) => {
      let amount = 0;
      let total = 0;
      state.cartItems.forEach((item) => {
        amount += item.amount;
        total += item.amount * item.price;
      });
      state.amount = amount;
      state.total = total;
    },
  },
});

export const { clearCart, removeItem, increase, decrease, calculateTotals } =
  cartSlice.actions;

export default cartSlice.reducer;
```

- CartItem.js

```js
import React from 'react';
import { ChevronDown, ChevronUp } from '../icons';

import { useDispatch } from 'react-redux';
import { removeItem, increase, decrease } from '../features/cart/cartSlice';

const CartItem = ({ id, img, title, price, amount }) => {
  const dispatch = useDispatch();

  return (
    <article className='cart-item'>
      <img src={img} alt={title} />
      <div>
        <h4>{title}</h4>
        <h4 className='item-price'>${price}</h4>
        {/* remove button */}
        <button
          className='remove-btn'
          onClick={() => {
            dispatch(removeItem(id));
          }}
        >
          remove
        </button>
      </div>
      <div>
        {/* increase amount */}
        <button
          className='amount-btn'
          onClick={() => {
            dispatch(increase({ id }));
          }}
        >
          <ChevronUp />
        </button>
        {/* amount */}
        <p className='amount'>{amount}</p>
        {/* decrease amount */}
        <button
          className='amount-btn'
          onClick={() => {
            if (amount === 1) {
              dispatch(removeItem(id));
              return;
            }
            dispatch(decrease({ id }));
          }}
        >
          <ChevronDown />
        </button>
      </div>
    </article>
  );
};

export default CartItem;
```

- App.js

```js
import { useEffect } from 'react';
import Navbar from './components/Navbar';
import CartContainer from './components/CartContainer';
import { useSelector, useDispatch } from 'react-redux';
import { calculateTotals } from './features/cart/cartSlice';

function App() {
  const { cartItems } = useSelector((state) => state.cart);
  const dispatch = useDispatch();
  useEffect(() => {
    dispatch(calculateTotals());
  }, [cartItems]);

  return (
    <main>
      <Navbar />
      <CartContainer />
    </main>
  );
}

export default App;
```

#### Modal

- create components/Modal.js

```js
const Modal = () => {
  return (
    <aside className='modal-container'>
      <div className='modal'>
        <h4>Remove all items from your shopping cart?</h4>
        <div className='btn-container'>
          <button type='button' className='btn confirm-btn'>
            confirm
          </button>
          <button type='button' className='btn clear-btn'>
            cancel
          </button>
        </div>
      </div>
    </aside>
  );
};
export default Modal;
```

- App.js

```js
return (
  <main>
    <Modal />
    <Navbar />
    <CartContainer />
  </main>
);
```

#### modal slice

- create features/modal/modalSlice.js

```js
import { createSlice } from '@reduxjs/toolkit';
const initialState = {
  isOpen: false,
};

const modalSlice = createSlice({
  name: 'modal',
  initialState,
  reducers: {
    openModal: (state, action) => {
      state.isOpen = true;
    },
    closeModal: (state, action) => {
      state.isOpen = false;
    },
  },
});

export const { openModal, closeModal } = modalSlice.actions;
export default modalSlice.reducer;
```

- App.js

```js
const { isOpen } = useSelector((state) => state.modal);

return (
  <main>
    {isOpen && <Modal />}
    <Navbar />
    <CartContainer />
  </main>
);
```

#### toggle modal

- CartContainer.js

```js
import { openModal } from '../features/modal/modalSlice';

return (
  <button
    className='btn clear-btn'
    onClick={() => {
      dispatch(openModal());
    }}
  >
    clear cart
  </button>
);
```

- Modal.js

```js
import { closeModal } from '../features/modal/modalSlice';
import { useDispatch } from 'react-redux';
import { clearCart } from '../features/cart/cartSlice';

const Modal = () => {
  const dispatch = useDispatch();

  return (
    <aside className='modal-container'>
      <div className='modal'>
        <h4>Remove all items from your shopping cart?</h4>
        <div className='btn-container'>
          <button
            type='button'
            className='btn confirm-btn'
            onClick={() => {
              dispatch(clearCart());
              dispatch(closeModal());
            }}
          >
            confirm
          </button>
          <button
            type='button'
            className='btn clear-btn'
            onClick={() => {
              dispatch(closeModal());
            }}
          >
            cancel
          </button>
        </div>
      </div>
    </aside>
  );
};
export default Modal;
```

#### async functionality with createAsyncThunk

- [Course API](https://course-api.com/)
- https://course-api.com/react-useReducer-cart-project
- cartSlice.js

- action type
- callback function
- lifecycle actions

```js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

const url = 'https://course-api.com/react-useReducer-cart-project';

export const getCartItems = createAsyncThunk('cart/getCartItems', () => {
  return fetch(url)
    .then((resp) => resp.json())
    .catch((err) => console.log(error));
});

const cartSlice = createSlice({
  name: 'cart',
  initialState,
  extraReducers: {
    [getCartItems.pending]: (state) => {
      state.isLoading = true;
    },
    [getCartItems.fulfilled]: (state, action) => {
      console.log(action);
      state.isLoading = false;
      state.cartItems = action.payload;
    },
    [getCartItems.rejected]: (state) => {
      state.isLoading = false;
    },
  },
});
```

- App.js

```js
import { calculateTotals, getCartItems } from './features/cart/cartSlice';

function App() {
  const { cartItems, isLoading } = useSelector((state) => state.cart);

  useEffect(() => {
    dispatch(getCartItems());
  }, []);

  if (isLoading) {
    return (
      <div className='loading'>
        <h1>Loading...</h1>
      </div>
    );
  }

  return (
    <main>
      {isOpen && <Modal />}
      <Navbar />
      <CartContainer />
    </main>
  );
}

export default App;
```

#### Options

```sh
npm install axios
```

- cartSlice.js

```js
export const getCartItems = createAsyncThunk(
  'cart/getCartItems',
  async (name, thunkAPI) => {
    try {
      // console.log(name);
      // console.log(thunkAPI);
      // console.log(thunkAPI.getState());
      // thunkAPI.dispatch(openModal());
      const resp = await axios(url);

      return resp.data;
    } catch (error) {
      return thunkAPI.rejectWithValue('something went wrong');
    }
  }
);
```

#### The extraReducers "builder callback" notation

cart/cartSlice

```js
const cartSlice = createSlice({
  name: 'cart',
  initialState,
  reducers: {
    // reducers
  },
  extraReducers: (builder) => {
    builder
      .addCase(getCartItems.pending, (state) => {
        state.isLoading = true;
      })
      .addCase(getCartItems.fulfilled, (state, action) => {
        // console.log(action);
        state.isLoading = false;
        state.cartItems = action.payload;
      })
      .addCase(getCartItems.rejected, (state, action) => {
        console.log(action);
        state.isLoading = false;
      });
  },
});
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🌐 Live Demo <a name="#live-demo"></a>
- [React Book Store Web App](https://benawi.github.io/Microverse-React-Bookstore/) 
- Learn More [How to deploy react app](https://github.com/gitname/react-gh-pages)
<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 💻 Getting Started with Create React App <a name="getting-started"></a>

To get a local copy up and running, follow these steps.

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Setup

Clone this repository to your desired folder:

> cd my-folder
> git clone git@github.com:Microverse-JS-Capstone.git

### Prerequisites

In order to run this project you need:

- gitHub account;
- git installed on your OS.

### Install

> [Linters](https://github.com/microverseinc/linters-config/tree/master/html-css-js)

- Installations required to run this project:

### Install the node module

- Run the following command:

```
npm install
```
### Creat the react 
[Create react app](https://create-react-app.dev/docs/getting-started)

- Run the following command:

```
npx create-react-app my-app
cd my-app
npm start
```

### In order to import a CSS file add the style-loader and css-loader to your module configuration

- Run the following command:

```
npm install --save-dev style-loader css-loader
```

### Webhint installation.

- Run the following command:

```
npm install --save-dev hint@7.x
```

### Stylelint installation.

- Run the following command:

```
npm install --save-dev stylelint@13.x stylelint-scss@3.x stylelint-config-standard@21.x stylelint-csstree-validator@1.x
```

### ESLint

- Run

```
npm install --save-dev eslint@7.x eslint-config-airbnb-base@14.x eslint-plugin-import@2.x babel-eslint@10.x
```

### Usage

You can use this project by cloning it to your folder and changing index.html and styles.css files.

### Run tests

To run tests, run the following commands:

To track linter errors locally follow these steps:

Download all the dependencies run:

```
npm install
```

Track HTML linter errors run:

```
npx hint .
```

Track CSS linter errors run:

```
npx stylelint "**/*.{css,scss}"
```

Track JavaScript linter errors run:

```
npx eslint .
```

### Deployment

You can redeploy this project by adding new lines of code to source files.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 👥 Authors <a name="authors"></a>

### 👤 Habtamu Alemayehu

- GitHub: [Benawi](https://github.com/Benawi)
- Linkdin: [Habtamu](https://www.linkedin.com/in/habtamu-alemayehu-b90367101/)


<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🔭 Future Features <a name="future-features"></a>

-  Add the reducers and actions in redux for adding and removing the books👌
-  Use the API for posting and fetching the books🚀
-  Add some animations style for the project💯
<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🤝 Contributing <a name="contributing"></a>

Contributions, [issues](https://github.com/Benawi/Microverse-React-Bookstore/issues), and feature requests are welcome!

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## ⭐️ Show your support <a name="support"></a>

Give me ⭐️ If you like this project!

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 🙏 Acknowledgments <a name="acknowledgements"></a>

- We would like to thank Microverse program for providing us this great chance.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## 📝 License <a name="license"></a>

This project is [MIT](./MIT.md) licensed.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
