# React Native

## Some Rules

- In the world of JSX, a starting tag must have an end tag


## Tags

- `<SafeAreaView>` is used to prevent the notch area in phones, the main app should be wrapped in a SafeAreaView tag to prevent components getting rendered in those areas

- `<View>` serves as an replacement of divs in the react native world.

- `<ScrollView>` is used wherever we want to have scrollability in the application, horizontal or vertical, it comes with props such as horizontal which we have to set to true



## Styling

```jsx
const styles = StyleSheet.create({
    supercontainer:{
        // overflow: 'scroll',
    },
    headingText: {
        fontSize: 24,
        fontWeight: 'bold',
        color: 'white',
    }});
```

We create an object like this and then we use it in the app like this


```jsx
<Myview style={styles.supercontainer} />
```


