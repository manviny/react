
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

    



## comnponents/_mini/index.js
```js

import React, { Component } from 'react';
import { connect } from 'react-redux';
import { Actions } from 'react-native-router-flux';
import { Container, Header, Title, Content, Text, Button, Icon, Left, Right, Body } from 'native-base';

import { openDrawer } from '../../actions/drawer';
import styles from './styles';

class _mini extends Component {



  render() {

    return (
        <Container>
        
            <Header>
                <Left>
                </Left>
                <Body>
                    <Title>{this.props.prueba}</Title>
                </Body>
                <Right>
                </Right>
            </Header>

            <Content>
                <Text>hola </Text>
            </Content>

        </Container>
 
    );
  }
}

function bindAction(dispatch) {
  return {
    openDrawer: () => dispatch(openDrawer()),
  };
}

const mapStateToProps = state => ({
  name: state.user.name,
  prueba: 'estado'
});


export default connect(mapStateToProps, bindAction)(_mini);

```

