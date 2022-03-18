<p align="center">
    <h1 align="center">Полезные дополнения</h1>
</p>

1. MPDf: для того что бы абзац не разрывался обернуть текст в div?, который будет перенес на новую страницу если границы выйдут (```<div style="margin-top: 8px; page-break-after: avoid; page-break-inside: avoid;">ВАШ ТЕКСТ </div>```) 
2. Регулярное выражение для проверки ФИО пример: "Иванов И" правило для Yii2 
```
[
    'field1_2',
    'match',
    'pattern' => '/^[А-Я]{1}[а-яё]{1,23}|[А-Я]{1}$/',
    'message' => 'Внесити в правиьном формате «Иванов И»',
]
```
3. Регулярное выражение для удаления всех пробелов в строке:
```
    $str_p = preg_replace('/\s+/', '', $out_save[$i][12]);
    $str_p = explode("/", $str_p);
```
4. Применение when и whenClient в правилах для Yii2 
```
[
    [
        'field43',
    ],
    'required',
    'when' => function ($model) {
        return $model->field42 == '1';
     },
     'whenClient' => "function (attribute, value) {
         return $('#detiankettable3544-field42').val() == '1';
      }",
]
```
5. Посмотреть запрос в форме sql для Yii2 (!! если запрос выдает результата сразу т.е. в конце стоит ->all() или ->one() то что бы сработал метод createCommand() ->all() или ->one()  нужно убрать!)
```
$rows = (new \yii\db\Query())
    ->select(
        [
            'id',
            'federal_district_id',
            'region_id',
            'municipality_id',
            'title',
             '(SELECT id from `director` where `director`.organization_id = `organization`.id) as result',
        ])
    ->from('organization')
    ->where($where)
     ->orderBy([
         'federal_district_id' => SORT_ASC,
         'region_id' => SORT_ASC,
         'municipality_id' => SORT_ASC,
     ])
$rows->createCommand()->rawSQL //покажет sql запрос
```
6. Посмотреть ошибки валидации для Yii2 
```
print_r('<pre>');
    foreach ($model->getErrors() as $key => $value) {
        print_r($key.': '.$value[0]);
        print_r('<br>');
    }
print_r(Yii::$app->request->post());
print_r('</pre>');
exit();
```
7. Время сессия для Yii2 (config/main.php)
Настройка php файлов пример https://snipp.ru/php/life-session
```
'user' => [
    'identityClass' => 'common\models\User',
    'enableAutoLogin' => true,
    'authTimeout' => 3600 * 15,
    'identityCookie' => ['name' => '_identity-backend', 'httpOnly' => true],
],
'session' => [
    'name' => 'advanced-backend',
    'timeout' => 3600*15,
],
```
8. Простой код для кнопки, на submit будет блокироваться, стили для bootstrap4
```
 $('form').on('beforeSubmit', function(){
        var form = $(this);
        var submit = form.find(':submit');
        submit.html('' +
            '<div class="spinner-border spinner-border-sm" role="status">'+
            '<span class="visually-hidden"></span>'+
            '</div> <strong> Пожалуйста, подождите...</strong>'
        );
        submit.prop('disabled', true);
    });
```
