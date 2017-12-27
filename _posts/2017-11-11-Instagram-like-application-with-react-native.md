---
layout: post
title:  "Instagram Like Application With React Native"
date:   2017-11-11
categories: mediator feature
image: /assets/article_images/2017-11-11-instagram-like-app-with-react-native/react-native.jpeg
---

This article is created to show people how to develop an Instagram like application with [React-native]("https://facebook.github.io/react-native/")

# What we will be building?

We are going to build an instagram like application using react native and this is how it is going to look like.

![image](/assets/article_images/2017-11-11-instagram-like-app-with-react-native/react-app-votepic.gif)

Although this application is not yet completed, for your reference, the code for this app I am building is available in this [Github repo]("https://github.com/clementpeihengtan/votepic")

# Let's Get Started

We will first need to create a new app. Open terminal and run these command to initialize a new project

```shell
$ react-native init votepic
$ cd votepic
```
# Install Dependencies

Next, install all necessary module, which will help us to build the application. We will need the modules below

- Icons for building the UX/UI
```terminal
$ npm install --save react-native-vector-icons
```
- Create transition between pages within the application 
```terminal
$ npm install --save react-navigation
```
- Tools set for extended component for React
```terminal
$ npm install --save native-base
```
- For type checking
```terminal
$ npm install --save prop-types
```
- Animation in page transition
```terminal
$ npm install --save react-native-animatable
$ npm install --save react-native-image-header-scroll-view
```

# Launch the Simulator

To launch the app in the simulator. Run the command below
```terminal
$ react-native run-ios
```
After launch, press <kbd>&#8984;</kbd> <kbd>D</kbd> and select Enable Hot Reloading to prevent us developer from manually reloading everytime we make a changes. 

# Data 

Let's create some data as a sample for our application. We're going to store all the pictures data in one file to make thing easier. In real world situation, we will need to fetch data by using API. 

- At your current directory create a file called <mark>data.json</mark> with the following content

```json
[
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name": "Rina Miele",
        "image_url": "https://media.wired.com/photos/5926538eaf95806129f4f0b6/master/pass/UnsplashHP.jpg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name" : "Kelsey Johnsen",
        "image_url": "https://1095.unsplash.com/img/videos/10.jpg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name": "Jessica Johns",
        "image_url": "https://i.pinimg.com/originals/57/80/0e/57800e6fd63b49c51c106bc26bbc3933.jpg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name": "John Cobb",
        "image_url": "https://cdn-images-1.medium.com/max/2000/1*YRINRZFr0E1FRJ4JpizEMw.jpeg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name" : "Samuel Scrimshaw",
        "image_url": "https://assets.awwwards.com/awards/images/2013/11/wall-unsplash-26-11-11.jpg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name" : "Tim Swaan",
        "image_url": "https://cdn.concreteplayground.com/content/uploads/2016/06/bikes-unsplash-bicycle-date-meghan-yabsley.jpg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name" : "Hollie Harmsworth",
        "image_url": "https://salemnet.vo.llnwd.net/media/cms/CW/Couples/singles/39078-man-handraised-sunset-unsplash.1200w.tn.jpg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name" : "Anton Darius",
        "image_url": "https://s3.amazonaws.com/s3.imagefinder.co/uploads/2016/01/27004234/unsplash-com-photo-1453284441168-8780c9f52097.jpg" ,
        "description": "Hi, guys! I am a photography enthusiast \n ood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name" : "Ales Krivec",
        "image_url": "https://i.pinimg.com/736x/d1/58/6d/d1586dad8532ca2ef76f23e59263b5ab--hd-photos-free-photos.jpg" ,
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    },
    {
        "profile_pic" : "https://images.unsplash.com/placeholder-avatars/extra-large.jpg",
        "name" : "Alberto Restifo",
        "image_url": "https://upload.wikimedia.org/wikipedia/commons/6/6d/City-streets-skyline-buildings_%2824326816445%29.jpg",
        "description": "Hi, guys! I am a photography enthusiast \nFood Lover"
    }
]
```

# Start Modifying the App

First, create a directory called <mark>src</mark>. In the directory, create two new directories called <mark>components</mark> and <mark>tabs</mark>

## Components
In the component directory, create a new file called <mark>Card.js</mark> that defines the container that display the user's image and information.

The code will look like this
```JavaScript
import React, {Component} from 'react';
import PropTypes from 'prop-types';
import {
    View,
    Text,
    Dimensions,
    StyleSheet,
    TouchableOpacity,
    Image
} from 'react-native';
import {
    Button,
    Icon
} from 'native-base';
import FontAwesome from 'react-native-vector-icons/FontAwesome'

export default class Card extends Component {
    static propTypes = {
        data: PropTypes.object.isRequired,
    }

    static defaultProps = {
        upbutton: 'caret-up'
    }

    render() {
        const {data, data: {profile_pic, name, image_url, description}, navigate} = this.props;
        return (
            <View style={styles.container}>
                <View style={styles.image_container}>
                        <Image source={{uri: profile_pic}} style={styles.pp} resizeMode="stretch"/>
                        <Text style={styles.text} onPress={()=>navigate('Profiles',data)}>{name}</Text>
                </View>
                <TouchableOpacity style={styles.container}>  
                    <View style={styles.pic_container}>
                        <Image source={{uri: image_url}} style={styles.image}/>
                    </View>
                </TouchableOpacity>
                <View style={styles.footer}>
                    <Button boarded black iconLeft light style={{width: 45, height: 30}}>
                        <Icon name='arrow-up' />
                    </Button>
                </View>
            </View>
        );
    }
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        marginBottom: 2
    },
    image_container: {
        flexDirection: "row",
        marginBottom: 10,
    },
    text : {
        marginTop: 5,
        marginBottom: 5,
        fontSize: 12,
    },
    pp: {
        marginRight: 10,
        marginLeft: 10,
        alignSelf: 'center',
        height: 25,
        width: 25,
        borderWidth: 0,
        borderRadius: 12
    },
    image: {
        ...StyleSheet.absoluteFillObject,
        width: null,
        height: null,
        alignItems: 'center',
        justifyContent:'center',
    },
    pic_container: {
        alignItems: 'stretch',
        height: 250
    },
    upicon: {
        alignSelf: 'center',
        height: 25,
        width: 25,
        borderWidth: 1,
        borderRadius: 5
    },
    footer: {
        margin: 8, 
        alignItems: 'stretch',
        marginBottom: 50
    }
});
```

And we are done for the component directory, just that easy!

## Tabs

Tabs directory will contains every pages in the application, which include 
- <mark>Home.js</mark> - Home page
- <mark>Profiles.js</mark> - Each user's profile
- <mark>Profile.js</mark> - The current user's profile

# Main page - App.js
Before we start modifying the tabs directory, we first need to create the basic of the application, which is the foundation that will assist in the navigation between different pages. 

- Open your <mark>App.js</mark> file
- The first thing that we need to do, is import all the necessary modules

```JavaScript 
import React, { Component } from 'react';
import {
  Platform,
  StyleSheet,
  Text,
  View
} from 'react-native';

import {
  StackNavigator,
  TabNavigator
} from 'react-navigation';      //To handle navigation between page
import Icon from 'react-native-vector-icons/Ionicons'; 
import FontAwesome from 'react-native-vector-icons/FontAwesome';
import Home from './tabs/Home';     //The home page we will create later
import Profiles from './tabs/Profiles'; //Every user's profile page
import Profile from './tabs/Profile'; //The current user profile page
```
Then we will need to add the code below
```JavaScript
const Homenav = StackNavigator({
  Home: {
    screen: Home,
    navigationOptions: {
      header: null,
    }
  }, 
  Profiles: {
    screen: Profiles,
    navigationOptions: ({navigation}) => ({
      // title: `${navigation.state.params.name}`,
      headerStyle:{ position: 'absolute', backgroundColor: 'transparent', zIndex: 100, top: 0, left: 0, right: 0, borderBottomWidth: 0, }
    })
  }
}, {
  headerMode: 'screen'
});

const App = TabNavigator({
  Home: {
    screen: Homenav,
    navigationOptions: {
      tabBarIcon: ({tintColor, focused}) => <Icon
        name={focused? 'ios-home' : 'ios-home-outline'}
        size={26}
        style={{color: '#000000'}}
      />
    }
  },
  Profile: {
    screen: Profile,
    navigationOptions: {
      tabBarIcon: ({tintColor, focused}) => <FontAwesome
        name={focused? 'user-circle' : 'user-circle-o'}
        size={26}
        style={{color: '#000000'}}
      />
    }
  }
},{
  tabBarOptions: {
    showLabel: false
  }
});

export default App;

```

## Home.js
Now we have completed the basis, we can now proceed to work on the tabs

- Open the <mark>Home.js</mark> file and write the code below

```JavaScript
import React, {Component} from 'react';
import {
    View,
    Text,
    ScrollView,
    StyleSheet
} from 'react-native'
import {
    Header,
    Container
} from 'native-base';

import Card from '../components/Card';
import info from '../../data.json';

export default class Home extends Component {
    render() {
        const {navigate} = this.props.navigation;
        return (
            <Container style={styles.container}>
                 <Header style={styles.header}>
                    {/*<MainButton onPress={() => navigate('DrawerOpen')}/>*/}
                    <Text style={styles.head}>Votepic</Text>
                </Header>
                <ScrollView>    
                    {info.map((data, index) => <Card
                    data = {data}
                    key={index}
                    navigate={navigate}
                    />
                    )}
                </ScrollView>
            </Container>
        );
    }
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#FFF'
    },
    header: {
        marginTop: 15,
        marginBottom: 10,
        flexDirection: 'row',
        backgroundColor: '#FFF',
        borderBottomWidth: 1
    },
    head: {
        marginTop: 8,
        fontSize: 20,
        justifyContent: 'center',
        alignItems: 'center'
    }
});
```

This file will handle creating a srollable view of list of <mark>Cards</mark> that we created previously. Upon completion, it will look like below

![images](https://github.com/clementpeihengtan/clement-tph/blob/gh-pages/assets/article_images/2017-11-11-instagram-like-app-with-react-native/home.png)

## Profiles.js
This page will be responsible in creating and displaying each user profile, based on what the current user has clicked.

```JavaScript
import React, {Component} from 'react';
import {
    View,
    Text,
    StyleSheet,
    Image,
    StatusBar,
    Dimensions
} from 'react-native';
import {Header} from 'react-navigation';
import * as Animatable from 'react-native-animatable';
import HeaderImageScrollView, { TriggeringView } from 'react-native-image-header-scroll-view';

export default class Profile extends Component {
    constructor(props) {
        super(props);
        this.state = {showNavTitle: false}
    }
    static navigationOptions = {
        headerStyle: {
            backgroundColor: '#FFF'
        }
    }

    render() {
        const {navigation, state:{params}} = this.props.navigation;
        return (
            <View style={{flex: 1}}>
                <StatusBar barStyle="light-content"/>
                <HeaderImageScrollView
                    maxHeight= {200}
                    minHeight= {50}
                    maxOverlayOpacity = {0.6}
                    minOverlayOpacity = {0.3}
                    fadeOutBackground
                    renderHeader = {() => <Image source={{uri: params.image_url}} style={styles.image}/>}
                    renderFixedForeground={() => 
                        <Animatable.View
                            style={styles.navTitleView}
                            ref = {
                                navTitleView =>{
                                    this.navTitleView = navTitleView;
                                }}
                        >
                        <Text style={styles.navTitle}>{params.name}</Text>
                        </Animatable.View>
                    }
                    renderForeground={() =>
                    <View style={styles.titleContainer}>
                    <Text style={styles.imageTitle}>
                        {params.name}
                    </Text>
                    </View>}
                >
                <TriggeringView>
                    <View style={styles.tab_section}>
                        <Image source={{uri: params.profile_pic}} style={styles.pp}/>
                        <Text style={styles.sectionContent}>{params.name}</Text>
                    </View>
                    <View style={styles.tab_section}>
                          <Text style={styles.sectionContent}>{params.description}</Text>
                    </View>
                </TriggeringView>

                </HeaderImageScrollView>
                {/*<View>
                    <Image source={{uri: params.profile_pic}}/>
                    <Text>{params.name}</Text>
                </View>
                <View>
                    
                </View>*/}
            </View>
        );
    }
}

const styles = StyleSheet.create({
  image: {
    height: 200,
    width: Dimensions.get('window').width,
    alignSelf: 'stretch',
    resizeMode: 'cover',
  },
  title: {
    fontSize: 20,
  },
  name: {
    fontWeight: 'bold',
  },
  section: {
    padding: 20,
    borderBottomWidth: 1,
    borderBottomColor: '#cccccc',
    backgroundColor: 'white',
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
  },
  sectionContent: {
    fontSize: 16,
    textAlign: 'justify',
  },
  keywords: {
    flexDirection: 'row',
    justifyContent: 'flex-start',
    alignItems: 'flex-start',
    flexWrap: 'wrap',
  },
  keywordContainer: {
    backgroundColor: '#999999',
    borderRadius: 10,
    margin: 10,
    padding: 10,
  },
  keyword: {
    fontSize: 16,
    color: 'white',
  },
  titleContainer: {
    flex: 1,
    alignSelf: 'stretch',
    justifyContent: 'center',
    alignItems: 'center',
  },
  imageTitle: {
    color: 'white',
    backgroundColor: 'transparent',
    fontSize: 24,
  },
  navTitleView: {
    height: 250,
    justifyContent: 'center',
    alignItems: 'center',
    paddingTop: 16,
    opacity: 0,
  },
  navTitle: {
    color: 'white',
    fontSize: 18,
    backgroundColor: 'transparent',
  },
  sectionLarge: {
    height: 600,
  },
  pp: {
        marginRight: 10,
        marginLeft: 10,
        alignSelf: 'center',
        height: 50,
        width: 50,
        borderWidth: 0,
        borderRadius: 12
  },
  tab_section: {
    flexDirection: "row",
    marginBottom: 10,
    marginTop: 20
  }
});
```


Upon completion, it will look like following when user click on different user name in the Home page.

![imaegs](https://github.com/clementpeihengtan/clement-tph/blob/gh-pages/assets/article_images/2017-11-11-instagram-like-app-with-react-native/profiles.png)


## Profile.js

Since this page is still in development phase, it is easy to show you guys how to create something like below using [native-base]("https://nativebase.io/")

![images](https://github.com/clementpeihengtan/clement-tph/blob/gh-pages/assets/article_images/2017-11-11-instagram-like-app-with-react-native/profile.png)

```JavaScript
import React, {Component} from 'react';
import { 
    Container, 
    Header, 
    Content, 
    List, 
    ListItem, 
    Text 
} from 'native-base';

export default class Profile extends Component {
    render() {
        return (
            <Container>
                <Header>
                    <Text>My Profile</Text>
                </Header>
                <Content>
                    <List>
                        <ListItem>
                            <Text>Login</Text>
                        </ListItem>
                        <ListItem>
                            <Text>Collection</Text>
                        </ListItem>
                    </List>
                </Content>
            </Container>
        );
    }
}
```

# Ta Da
How we have a simple Instagram like application, and I called it votepic. Hope you guys learn something from this tutorial. 







