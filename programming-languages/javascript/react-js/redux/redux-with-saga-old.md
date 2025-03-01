Before Redux Toolkit was introduced, Redux state management in React applications followed a more manual and boilerplate-heavy approach. Here’s a breakdown of how Redux state management worked with Redux and Redux-Saga before Redux Toolkit:


---

1. Install Dependencies

npm install redux react-redux redux-saga


---

2. Create Redux Actions

Actions represent events that trigger state updates.

actions.js

// Action Types
export const FETCH_DATA_REQUEST = 'FETCH_DATA_REQUEST';
export const FETCH_DATA_SUCCESS = 'FETCH_DATA_SUCCESS';
export const FETCH_DATA_FAILURE = 'FETCH_DATA_FAILURE';

// Action Creators
export const fetchDataRequest = () => ({ type: FETCH_DATA_REQUEST });
export const fetchDataSuccess = (data) => ({ type: FETCH_DATA_SUCCESS, payload: data });
export const fetchDataFailure = (error) => ({ type: FETCH_DATA_FAILURE, payload: error });


---

3. Create Redux Reducer

Reducers specify how the state changes in response to actions.

reducer.js

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


---

4. Create Redux-Saga Middleware

Sagas handle side effects such as API calls asynchronously.

sagas.js

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


---

5. Setup Redux Store with Saga Middleware

The store combines reducers and applies middleware for Redux-Saga.

store.js

import { createStore, applyMiddleware } from 'redux';
import createSagaMiddleware from 'redux-saga';
import dataReducer from './reducer';
import watchFetchDataSaga from './sagas';

const sagaMiddleware = createSagaMiddleware();

const store = createStore(dataReducer, applyMiddleware(sagaMiddleware));

sagaMiddleware.run(watchFetchDataSaga);

export default store;


---

6. Provide Store to React App

Wrap your application with the Redux provider.

index.js

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


---

7. Connect Redux State in React Component

Use useSelector to access state and useDispatch to trigger actions.

App.js

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


---

Summary

1. Actions - Define constants and action creators.


2. Reducer - Handle state updates based on actions.


3. Saga Middleware - Use redux-saga to manage async API calls.


4. Store - Create Redux store and apply saga middleware.


5. React Component - Connect Redux store with useSelector and useDispatch.



This method, though effective, required a lot of boilerplate code. Redux Toolkit simplifies this process by reducing boilerplate, improving structure, and integrating createSlice and createAsyncThunk for async logic.

Would you like to see a comparison with Redux Toolkit?

