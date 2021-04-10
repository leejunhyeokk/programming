# JS 문법

### if문

```javascript
if (조건부문) {
    동작부문
}

let temperature = 0;

if (temperature <= 0) {
    console.log('물이 언다')
} else {
    console.log('물이 얼지 않는다')
}
```



### else if문

```javascript
let temperature = 0;

if (temperature <= 0) {
    console.log('물이 언다')
} else if (temperature < 100) {
    console.log('물이 얼지도 끓지도 않는다')
} else if (temperature < 150) {
    console.log('물이 끓는다')
} else {
    console.log('물이 수증기가 되었다.')
}
```