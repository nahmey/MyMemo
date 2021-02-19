# My Memo for Dev

<!-- ![alt text](https://julien-kennel.fr/images/git/table.PNG) -->

Memo php, js, html, css, vue, laravel

- [Laravel](#laravel)
- [VueJS](#vuejs)
- [Javascript](#javascript)
- [Composer](#composer)
- [PHP](#php)
- [Postgres SQL](#postegres)


## Laravel

* Use function like usort with parameters in Laravel Class :
```php
private function date_compare($a, $b)
{
    $t1 = strtotime($a['date']);
    $t2 = strtotime($b['date']);
    return $t2 - $t1; 
}

usort($array, array($this,'date_compare'));
```

* Laravel Excel with Carbon (when import excel column date) :
```php
$row['my_date_column'] = Carbon::instance(\PhpOffice\PhpSpreadsheet\Shared\Date::excelToDateTimeObject($row['my_date_column']));
```

* Load Laravel helper (str_slug etc...) for laravel >= 6
```html
composer require laravel/helpers
```

* Configure Locale in Laravel :
Go to resources/lang/ ==> and create fr folder with translation
==> IMPORTANT : Copy/paste the fr.json in resources/lang/ and not in resources/lang/fr




## VueJS

* Check if user has role to access view
```javascript
//Route
{path: '/parametres', component: ParametresComponent, name:'parametres', meta: {roles:['admin', 'leads']}},

router.beforeEach((to, from, next) => {
    if(to.matched.some(record => record.meta.roles)){
        if(to.matched[0].meta.roles.indexOf(user.role) != -1) next();
        else next('/errors/404');
    }else next();
})
```


* Call 2 components in one view
```html
<!-- HTML -->
<div class="mb-2">
    <transition name="component-fade" mode="out-in">
        @if(\Auth::user()->hasRole('admin') || \Auth::user()->hasRole('leads'))
            <router-view name="default"></router-view>
        @else
            <router-view name="default" :key="$route.path"></router-view>
        @endif
    </transition>
</div>
```
```javascript
// App.js
{path: '/leads/suivi', component: LeadIndexComponent, meta: {roles:['admin', 'leads']},
    children: [{
        path: ':id',
        components: {second: LeadEditComponent},
    }]
},
```

* Global variable in app.js
```javascript
// App.js
Vue.prototype.$user = your data
// Exemple : Vue.prototype.$user = JSON.parse(document.querySelector("#app").dataset.user)
```

* Global function in app.js with examples
```javascript
const MyPlugin = {
    install(Vue, options){
        Vue.prototype.convertDate = (date) => {
            return moment(date).format('DD.MM.YYYY');
        }
        Vue.prototype.convertDateHour = (date) => {
            return moment(date).format('DD.MM.YYYY HH:mm');
        }
        Vue.prototype.convertHeure = (date) => {
            return moment(date).format('HH:mm');
        }
        Vue.prototype.datePickerOpened = (reference, $refs) => {
            $refs[reference].showCalendar();
            $refs[reference].$el.querySelector('input').focus();
        }
        // Check axios error and return what you want
        Vue.prototype.checkError = (error) => {
            if (error.response) {
                console.log(error.response.data);
                console.log(error.response.status);
                console.log(error.response.headers);
                if(error.response.status == 401){
                    ...
                }
                if(error.response.status == 403){
                    ...
                }
            }
        }
        // Get console error and post with XMLHttpRequest
        Vue.config.warnHandler = function(msg, vm, trace) {
            const token = document.querySelector('meta[name="csrf-token"]').getAttribute('content');
            var req = new XMLHttpRequest();
            let line = null;
            let url = null;
            var params = "msg=" + `Warn: ${msg}\nTrace: ${trace}` + '&amp;url=' + encodeURIComponent(url) + "&amp;line=" + line;
            req.open("POST", your_url, true);
            req.setRequestHeader('X-CSRF-Token', token);
            req.setRequestHeader('Content-type', 'application/x-www-form-urlencoded; charset=UTF-8');
            req.send(params);
        }
        // Check forms error from back-end and return with vue notify
        Vue.prototype.showErrors = (errors) => {
            let string = '<ul>';
            errors.forEach(function(item){
                string += '<li>'+item+'</li>';
            })
            string += '</ul>';

            Vue.notify({
                group: 'notifications',
                title: 'Erreur',
                type: 'error',
                duration: 5000,
                text: string
            });
        }
    }
}

Vue.use(MyPlugin)

```





## Javascript

* Check if button is double clicked
```javascript
function isDoubleClicked(element) {
    //if already clicked return TRUE to indicate this click is not allowed
    if (element.data("isclicked")) return true;

    //mark as clicked for 1 second
    element.data("isclicked", true);
    setTimeout(function () {
        element.removeData("isclicked");
    }, 1000);

    //return FALSE to indicate this click was allowed
    return false;
}
```

* Check all console error and post with XMLHttpRequest
```javascript
window.onerror = function(msg, url, line)
{
    const token = document.querySelector('meta[name="csrf-token"]').getAttribute('content');
    var req = new XMLHttpRequest();
    var params = "msg=" + encodeURIComponent(msg) + '&amp;url=' + encodeURIComponent(url) + "&amp;line=" + line;
    req.open("POST", base_url + "/admin/write_javacript_log", true);
    req.setRequestHeader('X-CSRF-Token', token);
    req.setRequestHeader('Content-type', 'application/x-www-form-urlencoded; charset=UTF-8');
    req.send(params);
};
```

## Composer

* Clear all cache (config, cache, view, route)
```html
php artisan optimize:clear
```


## Php

* Retrieves the years since a reference year (here 2020) based on the current year

```php
    public function getYears()
    {
        $debut = Carbon::createFromDate('2020');
        $this_year = Carbon::now()->format('Y');
        $diff = $debut->diffInYears($this_year);
        $annees = [$debut->format('Y')];

        for($i=0; $i < $diff ; $i++) {
            $annees[] = $debut->addYear()->format('Y');
        }

        return $annees;
    }
```


## Postgres

* Laravel + Postgres : active pdopgsql and pgsql on Wamp
    ==> IMPORTANT : go to C:/Wamp64/bin/php/your_php_version => php.ini and uncomment extension=pdo_pgsql and extension=pgsql
    ==> open console and verify with : php -m



<!-- ## Usage
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