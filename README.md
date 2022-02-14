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
],```
3. Применение when и whenClient в правилах для Yii2 
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
],```
 
