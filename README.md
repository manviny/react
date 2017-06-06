
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

