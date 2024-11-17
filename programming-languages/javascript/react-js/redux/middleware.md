# React Middleware

> In React, `middleware` typically refers to logic that intercepts actions or data at a certain point in the application's flow, allowing you to modify or perform tasks before proceeding.

![middleware workflow](https://miro.medium.com/v2/resize:fit:1400/1*AyYYoeDMTTK_7J7aCeaIUA.gif)

Although React itself doesn’t have built-in middleware like some backend frameworks,

- middleware in the context of React applications usually comes into play with state management libraries like `Redux` or `when handling API calls`.
- Middleware in redux is a `curried function 🥘🍛`

    ```javascript
    function someAction(a){
        return function (b) {
            return function (c){
                console.log(a, b, c)
            }
        }
    }

    someAction(a)(b)(c);
    ```

- In a React-Redux setup, middleware can be used to handle asynchronous actions, logging, error handling, and more.

## Custom Middleware in redux

```javascript
imports...

const logger = (store) => (next) => (action) => {
    console.log(store);
    console.log(next);
    console.log(action);

    next(action)
}
 
const store = configureStore({
    reducer: {
        // all reducers
    },
    middleware: [logger]
})
```

## Middleware in redux (libraries)

In a React-Redux setup, middleware can be used to handle asynchronous actions, logging, error handling, and more. Popular middleware for Redux includes `Redux Thunk` and `Redux Saga`.

### 1. Redux Thunk

**Purpose**: Allows you to write action creators that return functions instead of action objects. This is useful for handling asynchronous logic, such as API calls.

**Usage**:

```jsx
import thunk from 'redux-thunk';
import { createStore, applyMiddleware } from 'redux';
import rootReducer from './reducers';

const store = createStore(rootReducer, applyMiddleware(thunk));
```

```jsx
export const fetchData = () => {
  return async (dispatch) => {
    const response = await fetch('/api/data');
    const data = await response.json();
    dispatch({ type: 'FETCH_DATA_SUCCESS', payload: data });
  };
};
```

### 2. Redux saga

**Purpose**: A more powerful middleware for managing complex side effects in an application, such as handling concurrent requests and advanced workflows.

**Usage**:

```jsx
import createSagaMiddleware from 'redux-saga';
import { createStore, applyMiddleware } from 'redux';
import rootReducer from './reducers';
import rootSaga from './sagas';

const sagaMiddleware = createSagaMiddleware();
const store = createStore(rootReducer, applyMiddleware(sagaMiddleware));
sagaMiddleware.run(rootSaga);
```

```jsx
import { call, put, takeEvery } from 'redux-saga/effects';

function* fetchData() {
  try {
    const data = yield call(() => fetch('/api/data').then(res => res.json()));
    yield put({ type: 'FETCH_DATA_SUCCESS', payload: data });
  } catch (e) {
    yield put({ type: 'FETCH_DATA_FAILURE', message: e.message });
  }
}

function* watchFetchData() {
  yield takeEvery('FETCH_DATA_REQUEST', fetchData);
}

export default watchFetchData;
```
