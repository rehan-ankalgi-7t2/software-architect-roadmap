Before Redux Toolkit was introduced, Redux state management in React applications followed a more manual and boilerplate-heavy approach. Here’s a breakdown of how Redux state management worked with **Redux and Redux-Saga** before Redux Toolkit:

---

## **1. Install Dependencies**
```bash
npm install redux react-redux redux-saga
```

---

## **2. Create Redux Actions**  
Actions represent events that trigger state updates.

### `actions.js`
```js
// Action Types
export const FETCH_DATA_REQUEST = 'FETCH_DATA_REQUEST';
export const FETCH_DATA_SUCCESS = 'FETCH_DATA_SUCCESS';
export const FETCH_DATA_FAILURE = 'FETCH_DATA_FAILURE';

// Action Creators
export const fetchDataRequest = () => ({ type: FETCH_DATA_REQUEST });
export const fetchDataSuccess = (data) => ({ type: FETCH_DATA_SUCCESS, payload: data });
export const fetchDataFailure = (error) => ({ type: FETCH_DATA_FAILURE, payload: error });
```

---

## **3. Create Redux Reducer**  
Reducers specify how the state changes in response to actions.

### `reducer.js`
```js
import { FETCH_DATA_REQUEST, FETCH_DATA_SUCCESS, FETCH_DATA_FAILURE } from './actions';

const initialState = {
  data: [],
  loading: false,
  error: null,
};

const dataReducer = (state = initialState, action) => {
  switch (action.type) {
    case FETCH_DATA_REQUEST:
      return { ...state, loading: true, error: null };
    case FETCH_DATA_SUCCESS:
      return { ...state, loading: false, data: action.payload };
    case FETCH_DATA_FAILURE:
      return { ...state, loading: false, error: action.payload };
    default:
      return state;
  }
};

export default dataReducer;
```

---

## **4. Create Redux-Saga Middleware**  
Sagas handle side effects such as API calls asynchronously.

### `sagas.js`
```js
import { call, put, takeEvery } from 'redux-saga/effects';
import { FETCH_DATA_REQUEST, fetchDataSuccess, fetchDataFailure } from './actions';

// Mock API function
const fetchDataFromApi = async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  return response.json();
};

// Worker saga
function* fetchDataSaga() {
  try {
    const data = yield call(fetchDataFromApi);
    yield put(fetchDataSuccess(data)); // Dispatch success action
  } catch (error) {
    yield put(fetchDataFailure(error.message)); // Dispatch failure action
  }
}

// Watcher saga
function* watchFetchDataSaga() {
  yield takeEvery(FETCH_DATA_REQUEST, fetchDataSaga);
}

export default watchFetchDataSaga;
```

---

## **5. Setup Redux Store with Saga Middleware**  
The store combines reducers and applies middleware for Redux-Saga.

### `store.js`
```js
import { createStore, applyMiddleware } from 'redux';
import createSagaMiddleware from 'redux-saga';
import dataReducer from './reducer';
import watchFetchDataSaga from './sagas';

const sagaMiddleware = createSagaMiddleware();

const store = createStore(dataReducer, applyMiddleware(sagaMiddleware));

sagaMiddleware.run(watchFetchDataSaga);

export default store;
```

---

## **6. Provide Store to React App**
Wrap your application with the Redux provider.

### `index.js`
```js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

---

## **7. Connect Redux State in React Component**
Use `useSelector` to access state and `useDispatch` to trigger actions.

### `App.js`
```js
import React, { useEffect } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { fetchDataRequest } from './actions';

const App = () => {
  const dispatch = useDispatch();
  const { data, loading, error } = useSelector((state) => state);

  useEffect(() => {
    dispatch(fetchDataRequest());
  }, [dispatch]);

  return (
    <div>
      <h1>Redux Saga Example</h1>
      {loading && <p>Loading...</p>}
      {error && <p>Error: {error}</p>}
      <ul>
        {data.map((item) => (
          <li key={item.id}>{item.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default App;
```

---

## **Summary**
1. **Actions** - Define constants and action creators.
2. **Reducer** - Handle state updates based on actions.
3. **Saga Middleware** - Use `redux-saga` to manage async API calls.
4. **Store** - Create Redux store and apply saga middleware.
5. **React Component** - Connect Redux store with `useSelector` and `useDispatch`.

---

## Example: Expense management app 🪙
Let’s build an **Expense Management App** using Redux and Redux-Saga (the old way before Redux Toolkit). This app will allow users to:  

✅ Add a new expense  
✅ Fetch all expenses from an API (mocked)  
✅ Handle loading and error states  

---

## **1️⃣ Install Dependencies**
```bash
npm install redux react-redux redux-saga
```

---

## **2️⃣ Define Action Types & Creators**  
Actions trigger state updates in the reducer.

### 📄 `actions.js`
```js
// Action Types
export const ADD_EXPENSE = 'ADD_EXPENSE';
export const FETCH_EXPENSES_REQUEST = 'FETCH_EXPENSES_REQUEST';
export const FETCH_EXPENSES_SUCCESS = 'FETCH_EXPENSES_SUCCESS';
export const FETCH_EXPENSES_FAILURE = 'FETCH_EXPENSES_FAILURE';

// Action Creators
export const addExpense = (expense) => ({
  type: ADD_EXPENSE,
  payload: expense,
});

export const fetchExpensesRequest = () => ({
  type: FETCH_EXPENSES_REQUEST,
});

export const fetchExpensesSuccess = (expenses) => ({
  type: FETCH_EXPENSES_SUCCESS,
  payload: expenses,
});

export const fetchExpensesFailure = (error) => ({
  type: FETCH_EXPENSES_FAILURE,
  payload: error,
});
```

---

## **3️⃣ Create a Reducer**  
Reducers update the state based on dispatched actions.

### 📄 `reducer.js`
```js
import {
  ADD_EXPENSE,
  FETCH_EXPENSES_REQUEST,
  FETCH_EXPENSES_SUCCESS,
  FETCH_EXPENSES_FAILURE,
} from './actions';

const initialState = {
  expenses: [],
  loading: false,
  error: null,
};

const expenseReducer = (state = initialState, action) => {
  switch (action.type) {
    case ADD_EXPENSE:
      return {
        ...state,
        expenses: [...state.expenses, action.payload],
      };

    case FETCH_EXPENSES_REQUEST:
      return { ...state, loading: true, error: null };

    case FETCH_EXPENSES_SUCCESS:
      return { ...state, loading: false, expenses: action.payload };

    case FETCH_EXPENSES_FAILURE:
      return { ...state, loading: false, error: action.payload };

    default:
      return state;
  }
};

export default expenseReducer;
```

---

## **4️⃣ Create a Redux-Saga Middleware**  
Sagas handle asynchronous tasks like API calls.

### 📄 `sagas.js`
```js
import { call, put, takeEvery } from 'redux-saga/effects';
import {
  FETCH_EXPENSES_REQUEST,
  fetchExpensesSuccess,
  fetchExpensesFailure,
} from './actions';

// Mock API call
const fetchExpensesFromApi = async () => {
  return new Promise((resolve) =>
    setTimeout(() => resolve([{ id: 1, title: 'Groceries', amount: 500 }]), 1000)
  );
};

// Worker Saga: Fetch expenses
function* fetchExpensesSaga() {
  try {
    const expenses = yield call(fetchExpensesFromApi);
    yield put(fetchExpensesSuccess(expenses)); // Dispatch success action
  } catch (error) {
    yield put(fetchExpensesFailure(error.message)); // Dispatch failure action
  }
}

// Watcher Saga: Watches for FETCH_EXPENSES_REQUEST action
function* watchFetchExpensesSaga() {
  yield takeEvery(FETCH_EXPENSES_REQUEST, fetchExpensesSaga);
}

export default watchFetchExpensesSaga;
```

---

## **5️⃣ Create the Redux Store**  
The store manages global state.

### 📄 `store.js`
```js
import { createStore, applyMiddleware } from 'redux';
import createSagaMiddleware from 'redux-saga';
import expenseReducer from './reducer';
import watchFetchExpensesSaga from './sagas';

const sagaMiddleware = createSagaMiddleware();

const store = createStore(expenseReducer, applyMiddleware(sagaMiddleware));

sagaMiddleware.run(watchFetchExpensesSaga);

export default store;
```

---

## **6️⃣ Provide Redux Store to React App**  
Wrap the application with Redux **Provider**.

### 📄 `index.js`
```js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

---

## **7️⃣ Create the Expense Management Component**
Use `useSelector` to access Redux state and `useDispatch` to trigger actions.

### 📄 `App.js`
```js
import React, { useEffect, useState } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { fetchExpensesRequest, addExpense } from './actions';

const App = () => {
  const dispatch = useDispatch();
  const { expenses, loading, error } = useSelector((state) => state);

  const [title, setTitle] = useState('');
  const [amount, setAmount] = useState('');

  useEffect(() => {
    dispatch(fetchExpensesRequest());
  }, [dispatch]);

  const handleAddExpense = () => {
    if (title && amount) {
      dispatch(addExpense({ id: Date.now(), title, amount: Number(amount) }));
      setTitle('');
      setAmount('');
    }
  };

  return (
    <div>
      <h1>Expense Management</h1>

      {/* Add Expense Form */}
      <input
        type="text"
        placeholder="Expense Title"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
      />
      <input
        type="number"
        placeholder="Amount"
        value={amount}
        onChange={(e) => setAmount(e.target.value)}
      />
      <button onClick={handleAddExpense}>Add Expense</button>

      {/* Loading & Error Handling */}
      {loading && <p>Loading...</p>}
      {error && <p>Error: {error}</p>}

      {/* Expense List */}
      <ul>
        {expenses.map((expense) => (
          <li key={expense.id}>
            {expense.title}: ₹{expense.amount}
          </li>
        ))}
      </ul>
    </div>
  );
};

export default App;
```

---

## **🎯 Summary**
1️⃣ **Actions** – Define `ADD_EXPENSE`, `FETCH_EXPENSES_REQUEST`, etc.  
2️⃣ **Reducer** – Manage state updates for `expenses`, `loading`, and `error`.  
3️⃣ **Redux-Saga** – Handle async API calls with `call()`, `put()`, and `takeEvery()`.  
4️⃣ **Store** – Combine reducer and apply `sagaMiddleware`.  
5️⃣ **React Component** – Connect Redux using `useSelector()` and `useDispatch()`.  

---

## **🔥 Why Redux Toolkit is Better?**
- **Less boilerplate** – Fewer files and cleaner code.  
- **Built-in async handling** – `createAsyncThunk` simplifies API calls.  
- **Slices** – `createSlice` combines actions and reducers in one place.  
