npm i redux --save
npm i react-redux --save

src
	actions
	components
	reducers
	store.js

store.js
	import { createStore } from 'redux';
	import { rootReducer } from './reducers';
	export default(initialState) => {
		return createStore(rootReducer, initialState);
	}

/reducers/index.js
	import cart from ''