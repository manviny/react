
    .
    ├── ...
    ├── actions                     
    │   ├── user.js                 
    │   ├── _mini.js                # Definir actions
    │   ├── types.js                # NECESARIO -> registrar action
    │   └── ...                     
    ├── components                   
    │   ├── login           
    │   │   ├── index.js  
    │   │   ├── styles.js  
    │   ├── _mini          
    │   │   ├── index.js            # Componente
    │   │   ├── styles.js       
    │   ├── ... 
    ├── reducers                    
    │   ├── index.js                # NECESARIO -> combineReducers              
    │   ├── user.js   
    │   ├── _mini.js                # reducer
    │   └── ...      
    ├── App.js                     
    ├── AppNavigator.js             # NECESARIO -> navegacion
    ├── configureStore.js 
    ├── promise.js
    ├── setup.js    
    └── ...

# Actions
## actions/_mini.js
```js
// 	añadir en types.js
// 		| { type: 'SET_MINI', name: string}


import type { Action } from './types';

export const SET_MINI = 'SET_MINI';

export function setMini(mini:string):Action {
  return {
    type: SET_MINI,
    payload: mini,
  };
}
```    

## actions/types.js
```js
export type Action =
  { type: 'PUSH_NEW_ROUTE', route: string }
  
    ...
  
    | { type: 'SET_USER', name: string}
    | { type: 'SET_MINI', name: string}

    ...

export type Dispatch = (action:Action | Array<Action>) => any;
export type GetState = () => Object;
export type PromiseAction = Promise<Action>;
```


# Component
## components/_mini/index.js
```js


import React, { Component } from 'react';
import { connect } from 'react-redux';
import { Actions } from 'react-native-router-flux';
import { Container, Header, Title, Content, Text, Button, Icon, Left, Right, Body } from 'native-base';

import { openDrawer } from '../../actions/drawer';
import { setMini } from '../../actions/_mini';
import styles from './styles';

class _mini extends Component {


  render() {
    return (

        <Container>
            <Header>
                <Left> </Left>

                <Body>
                    <Title>{this.props.titulo}</Title>
                </Body>

                <Right> </Right>
            </Header>

            <Content>
                <Text>hola {this.props.mini}</Text>
             
                <Button transparent onPress={() => this.props.setMini('texto al hacer click')}>
                   <Icon name="pin" />
                </Button>                
            </Content>

        </Container>
 
    );
  }
}

function bindAction(dispatch) {
  return {
    setMini: mini => dispatch(setMini(mini)),
  };
}

const mapStateToProps = state => ({
  titulo: 'estado',
  mini: state.mini.mini,
});


export default connect(mapStateToProps, bindAction)(_mini);


```
# Reducers
## reducers/index.js
```js
import { combineReducers } from 'redux';

import user from './user';

    ...

import mini from './_mini';

    ...

export default combineReducers({
  user,
  mini,
 
});


```

## reducers/_mini.js
```js
// 	Añadir en /reducers/index.js
//	combineReducers =>las lineas necesarias

import type { Action } from '../actions/types';
import { SET_MINI } from '../actions/_mini';

export type State = {
    mini: string
}

const initialState = {
  mini: 'texto al inicializar',
};

export default function (state:State = initialState, action:Action): State {
  if (action.type === SET_MINI) {
    return {
      ...state,
      mini: action.payload,
    };
  }
  return state;
}

```
#  App Router
## AppNavigator.js
```js
...
import _mini from './components/_mini';
...
_renderScene(props) {
...
      case '_mini':
        return <_mini />;
...
        <RouterWithRedux>
          <Scene key="root">
          ...
          <Scene key="_mini" component={_mini} />
          ...

```
