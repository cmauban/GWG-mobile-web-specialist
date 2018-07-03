# Ajax with jQuery

## `.ajax()` Method

```javascript
$.ajax(<url-to-fetch>, <a-configuration-object>);

// or the more common way..

$.ajax(<just a configuration object>);

```
* **Configuration Objection** - plain javascript obj that's used to configure someting. for example:
    ```javascript
    var settings = {
       frosting: 'buttercream',
       colors: ['orange', 'blue'],
       layers: 2,
       isRound: true
    };
    ```
A simple Ajax request:
```javascript
$.ajax({
    url: 'https://swapi.co/api/people/1/'
});
```
