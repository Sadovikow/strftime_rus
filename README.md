# strftime_rus
Переформатирование даты в родительный падеж


```php
function strftime_rus($format, $date = FALSE) {
    // Работает точно так же, как и strftime(),
    // только в строке формата может принимать
    // дополнительный аргумент %B2, который будет заменен
    // на русское название месяца в родительном падеже.

    // В остальном правила для $format такие же, как и для strftime().
    // (в связи с этим рекомендуется настроить выполнение скрипта
    // с помощью setlocale: http://php.net/setlocale)

    // Второй аргумент можно передавать как в виде временной метки
    // так и в виде строки типа 2010-05-16 23:48:20
    // функция сама определит, в каком виде передана дата,
    // и проведет преобразование.
    // Если второй аргумент не указан,
    // функция будет работать с текущим временем.

    if (!$date)
        $timestamp = time();

    elseif (!is_numeric($date))
        $timestamp = strtotime($date);

    else
        $timestamp = $date;

    if (strpos($format, '%B2') === FALSE)
        return strftime($format, $timestamp);

    $month_number = date('n', $timestamp);

    switch ($month_number) {
        case 1: $rus = 'января'; break;
        case 2: $rus = 'февраля'; break;
        case 3: $rus = 'марта'; break;
        case 4: $rus = 'апреля'; break;
        case 5: $rus = 'мая'; break;
        case 6: $rus = 'июня'; break;
        case 7: $rus = 'июля'; break;
        case 8: $rus = 'августа'; break;
        case 9: $rus = 'сентября'; break;
        case 10: $rus = 'октября'; break;
        case 11: $rus = 'ноября'; break;
        case 12: $rus = 'декабря'; break;
    }

    $rusformat = str_replace('%B2', $rus, $format);

    return strftime($rusformat, $timestamp);
}
```
