
# All about redux-toolkit

# 1
----------------
### src/app/store.js

```javascript
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from '../features/counter/CounterSlice'
export const store = configureStore({
    reducer: {
        counter: counterReducer
    }
})

```
### main.jsx
```javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import { Provider } from 'react-redux'
import App from './App'
import { store } from './app/store'
import './index.css'


ReactDOM.createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </Provider>,
)

```
### src/features/counter/CounterSlice.js

```javascript
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
    value: 0
}

export const counterSlice = createSlice({
    name: 'counter',
    initialState,
    reducers: {
        increment: (state) => {
            state.value = state.value + 1
        },
        decrement: (state) => {
            state.value = state.value - 1
        },
        reset: (state) => {
            state.value = 0
        },
        incremtByNum: (state, action) => {
            state.value = state.value + action.payload
        },
        incrementYouWant: (state, action) => {
            state.value = state.value + action.payload
        }
    }
})

export const { increment, decrement, reset, incremtByNum, incrementYouWant } = counterSlice.actions
export default counterSlice.reducer

```


### src/components/Counter.jsx
```javascript
import React,{useState} from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { increment, decrement, reset, incremtByNum, incrementYouWant } from '../features/counter/CounterSlice'

const Counter = () => {
    const countValue = useSelector(state=> state.counter.value)
    const dispatch = useDispatch()

    const [wantedNum, setWantedNum] = useState(0)

    const addedNum = Number(wantedNum)
  return (
    <div>
        <h1>count: {countValue}</h1>
        <button onClick={()=> dispatch(increment())}>+</button>
        <button onClick={()=> dispatch(incremtByNum(5))}>increment by 5</button>
        <button onClick={()=> dispatch(decrement())}>-</button>
        <button onClick={() => dispatch(reset())}>reset</button>
        <br /> <br /><br />
        
            <input type="text" onChange={(e)=> setWantedNum(e.target.value)}/>
            <button onClick={()=> dispatch(incrementYouWant(addedNum))}>want</button>
       
    </div>
  )
}

export default Counter

```


#### Here is the output

![Logo](https://i.ibb.co/KKpxmHV/Screenshot-20230202-092241.png)





