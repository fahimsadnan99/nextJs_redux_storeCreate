# nextJs_redux_storeCreate

## first Install pakage 
### npm i redux react-redux redux-thunk next-redux-wrapper redux-devtools-extension

 than create Reducer,Action, Constant and Store 
 
 heare Sotore Code 
 
 //Sotore Code
 
 # Store Component
 
    import { createStore, applyMiddleware } from "redux"
    import { createWrapper, HYDRATE } from "next-redux-wrapper"
    import thunkMiddleWare from "redux-thunk"
    import reducers from "./Reducer/reducers";

    const bindMiddleware = (middleware) => {
       if (process.env.NODE_ENV !== 'production') {
           const { composeWithDevTools } = require('redux-devtools-extension')
           return composeWithDevTools(applyMiddleware(...middleware))
       }

       return applyMiddleware(...middleware)
    }


    const reducer = (state, action) => {
       if (action.type === HYDRATE) {
           const nextState = {
               ...state,
              ...action.payload
           }

           return nextState
       } else {
       //reducers is rootReducer Component - Here combine All reducer
           return reducers(state, action)
       }
    }

    const initStore = () => {
       return createStore(reducer,bindMiddleware([thunkMiddleWare]))
    }

    export const wrapper = createWrapper(initStore)
