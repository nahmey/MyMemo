# My Memo for Dev

<!-- ![alt text](https://julien-kennel.fr/images/git/table.PNG) -->

Memo php, js, html, css, vue, laravel

- [Laravel](#laravel)
<!-- - [Installation](#installation)
- [Usage](#example-usage)
- [Retrieve Data](#retrieve-data)
- [Props](#props)
- [Example](#example) -->

## Laravel
Use function like usort with parameters in Laravel Class :
```php
private function date_compare($a, $b)
{
    $t1 = strtotime($a['date']);
    $t2 = strtotime($b['date']);
    return $t2 - $t1; 
}

usort($array, array($this,'date_compare'));
```


<!-- ## Installing

Install with npm:
```bash
npm i light-vue-timepicker
```

Import globally in app.js:

```javascript
import LightVueTimepicker from 'light-vue-timepicker';
Vue.component('light-vue-timepicker', LightVueTimepicker);



```

## Usage
```html
<light-vue-timepicker></light-vue-timepicker>
```

## Retrieve data

```javascript
variable = {
	yourVmodel.hour,
	yourVmodel.minute,
	yourVmodel.second,
	yourVmodel.a
}
```

## Props

| Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Type | Description | Default
| ----------------- | :--- | :--- | :--- |
| `hourRange`      | `Array` | Range of hours which displayed (ex ['8-12', '14-19', '22']) | ['00-23'] |
| `minuteRange`      | `Array` | Range of minutes which displayed (ex ['0-30']) | ['00-59'] |
| `secondRange`      | `Array` | Range of secondes which displayed (ex ['0-30']) | ['00-59'] |
| `classe`      | `String` | class(boostrap or other) for input hour and minute | form-control col-5 |
| `format`      | `String` | Format 12 or 24 | 24 |
| `lang`      | `String` | lang fr or en  | null (display HH MM) |
| `withHour`      | `Boolean` | Display input hour  | true |
| `withMinute`      | `Boolean` | Display input minute  | true |
| `withSecond`      | `Boolean` | Display input second  | false |


## Example
```html
<light-vue-timepicker
v-model="time"
lang="en"
:hourRange="['8-12', '14-19', '21']"
:minuteRange="['30', '40', '55-57']"
:withSecond="true"
>
</light-vue-timepicker>
``` -->