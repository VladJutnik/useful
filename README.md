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
9. Добавление в массив js элемент массива и элемент в массив как объект   
```
arr.push(arr[listItemReady[k].id])
data.push({
    idRow: rowItems[i].id,
    col: col
})
```
9. Раскидываение j,]trnjd   
```
let fff = [
            {
                idRow: "1",
                nameRow: "Название области",
                col: [
                    {
                        idCol: "row1/col1",
                        element: [
                            {id: 1,textInput: "wdwdwd",type: "input"}
                        ]
                    }
                ]
            },
            {
                idRow: "2",
                nameRow: "Название области",
                col: [
                    {
                        idCol: "row2/col1",
                        element: [
                            {id: 4, type: 'date', textInput: 'efefefefef'},
                            {id: 6, type: 'input', textInput: 'gggggggggg'},
                            {id: 7, type: 'input', textInput: 'ffff'},
                        ]
                    },
                    {
                        idCol: "row2/col2",
                        element: [
                            {id: 2, type: 'date', textInput: 'wdwdwd'}
                        ]
                    },
                    {
                        idCol: "row2/col3",
                        element: [
                            {id: 8, type: 'input', textInput: 'ffff'},
                            {id: 3, type: 'input', textInput: 'efefefef'}
                        ]
                    }
                ]
            }
        ]
        function preview()
        {
            let content = '';
            if(data !== []){
                //console.log(data)
                content += '<div class="container-fluid rounded border border-primary">'
                data.forEach(function(item, i, arr) {
                    //console.log(item.col)
                    content += '<div class="row">'
                    content += `<h5 class="text-center mb-2">${item.nameRow}</h5>`
                    if(item.col.length === 1){
                        item.col.forEach(function(item, i, arr) {
                            //console.log(item)
                            content += '<div class="col-12">'
                            item.element.forEach(function(item, i, arr) {
                                //console.log(item)
                                if(item.type === "input"){
                                    content += `
                                        <label for="${item.id}">${item.textInput}</label>
                                        <input type="text" class="form-control" id="${item.id}">
                                        <br>
                                    `
                                }
                                else if(item.type === "date"){
                                    content += `
                                        <label for="${item.id}">${item.textInput}</label>
                                        <input type="date" class="form-control " id="${item.id}">
                                        <br>
                                    `
                                }
                            })
                            content += '</div>'
                        })
                    }
                    else if(item.col.length === 2){
                        item.col.forEach(function(item, i, arr) {
                            //console.log(item)
                            content += '<div class="col-6">'
                            item.element.forEach(function(item, i, arr) {
                                //console.log(item)
                                if(item.type === "input"){
                                    content += `
                                        <label for="${item.id}">${item.textInput}</label>
                                        <input type="text" class="form-control" id="${item.id}">
                                        <br>
                                    `
                                } else if(item.type === "date"){
                                    content += `
                                        <label for="${item.id}">${item.textInput}</label>
                                        <input type="date" class="form-control " id="${item.id}">
                                        <br>
                                    `
                                }
                            })
                            content += '</div>'
                        })
                    }
                    else {
                        item.col.forEach(function(item, i, arr) {
                            //console.log(item)
                            content += '<div class="col-4">'
                            item.element.forEach(function(item, i, arr) {
                                //console.log(item)
                                if(item.type === "input"){
                                    content += `
                                        <label for="${item.id}">${item.textInput}</label>
                                        <input type="text" class="form-control" id="${item.id}">
                                        <br>
                                    `
                                } else if(item.type === "date"){
                                    content += `
                                        <label for="${item.id}">${item.textInput}</label>
                                        <input type="date" class="form-control " id="${item.id}">
                                        <br>
                                    `
                                }
                            })
                            content += '</div>'
                        })
                    }
                    content += '</div><br>'
                })
                content += '</div>'
            } else {
                content += `
                    <div class="alert alert-danger text-center font-weight-bold" role="alert">
                        Данных на странице не найдено! Добавьте колонки и элементы на страницу!
                    </div>`
            }
            $('#result').html(content);
        }
```
10. Перенос всего абзаца на следующию страницу если часть обзаца разорвалась в Mpdf 
```
<div style="margin-top: 8px; page-break-after: avoid; page-break-inside: avoid;"></div>
```
11. Запрос выборка по дате, которая храниться в формате INT 
```
SELECT
    *
FROM `medicals`
inner join kids on medicals.kids_id = kids.id
inner join organization on kids.organization_id = organization.id
inner join type_lager on organization.type_lager_id = type_lager.id
WHERE CONVERT(FROM_UNIXTIME(medicals.date), DATETIME) BETWEEN '2020-07-14' and '2020-07-15';
```
12. Кастом правило в rules() для Yii2 
```
[
    [
        'field31_1_1',
        'field31_1_2',
        'field31_2_1',
        'field31_2_2',
        'field31_3_1',
    ], function ($attribute, $params) {
        $sum =
            $this->field31_1_1 +
            $this->field31_1_2 +
            $this->field31_2_1 +
            $this->field31_2_2 +
            $this->field31_3_1;

        if ($sum > 1) {
            $this->addError($attribute, 'Проверьте правильность внесения, в столбце может быть только один ответ: "ДА" ');
        }
    }
],
```
13. Кастом правило в rules() для Yii2 с выносом в отдельную функцию 
```

[
    [
        'field4_1',
        'field4_2',
        'field4_3',
        'field4_21',
        'field4_22',
        'field4_23',
    ],
    'validateSum','message'=>'Проверьте правильность суммы'
],

public function validateSum($attribute)
{
    $rules_array_sum = [
        'field4_1' => ['==', 'field4_5', 'field4_9', 'field4_13'],
        'field4_2' => ['==', 'field4_6', 'field4_10', 'field4_14'],
        'field4_3' => ['==', 'field4_7', 'field4_11', 'field4_15'],
        'field4_21' => ['==', 'field4_1', 'field4_17'],
        'field4_22' => ['==', 'field4_2', 'field4_18'],
        'field4_23' => ['==', 'field4_3', 'field4_19'],
        /*'field5' => ['<=', 'field4'],
        'field5' => ['<=', 'field4'],*/
    ];
    //print_r(count($rules_array_sum[$attribute])); exit();
    $sum = 0;
    for ($i = 0, $count_info = count($rules_array_sum[$attribute]) - 1; $count_info > 0; $count_info--, $i++) {
        $sum = $sum + $this[$rules_array_sum[$attribute][$i + 1]];
    }
    switch ($rules_array_sum[$attribute][0]) {
        case '==':
            if ((int)$this->$attribute !== (int)$sum) {
                $this->addError(
                    $attribute,
                    'У Вас ошибка по '.$rules_array_sum[$attribute][0].' выделенных строк'
                );
                for (
                    $j = 0, $count_info = count(
                        $rules_array_sum[$attribute]
                    ) - 1; $count_info > 0; $count_info--, $j++
                ) {
                    $this->addError(
                        $rules_array_sum[$attribute][$j + 1],
                        'Ошибка, проверьте правильность внесения: '.$this->getAttributeLabel(
                            $rules_array_sum[$attribute][$j + 1]
                        ).';'
                    );
                }
            }
            break;
        case '<=':
            if ((int)$this->$attribute > (int)$sum) {
                $this->addError(
                    $attribute,
                    'У Вас ошибка по '.$rules_array_sum[$attribute][0].' выделенных строк'
                );
                for (
                    $j = 0, $count_info = count(
                        $rules_array_sum[$attribute]
                    ) - 1; $count_info > 0; $count_info--, $j++
                ) {
                    $this->addError(
                        $rules_array_sum[$attribute][$j + 1],
                        'Ошибка, проверьте правильность внесения: '.$this->getAttributeLabel(
                            $rules_array_sum[$attribute][$j + 1]
                        ).';'
                    );
                }
            }
            break;
        case '<':
            if ((int)$this->$attribute >= (int)$sum) {
                $this->addError(
                    $attribute,
                    'У Вас ошибка по '.$rules_array_sum[$attribute][0].' выделенных строк'
                );
                for (
                    $j = 0, $count_info = count(
                        $rules_array_sum[$attribute]
                    ) - 1; $count_info > 0; $count_info--, $j++
                ) {
                    $this->addError(
                        $rules_array_sum[$attribute][$j + 1],
                        'Ошибка, проверьте правильность внесения: '.$this->getAttributeLabel(
                            $rules_array_sum[$attribute][$j + 1]
                        ).';'
                    );
                }
            }
            break;
        case '>':
            if ((int)$this->$attribute <= (int)$sum) {
                $this->addError(
                    $attribute,
                    'У Вас ошибка по '.$rules_array_sum[$attribute][0].' выделенных строк;'
                );
                for (
                    $j = 0, $count_info = count(
                        $rules_array_sum[$attribute]
                    ) - 1; $count_info > 0; $count_info--, $j++
                ) {
                    $this->addError(
                        $rules_array_sum[$attribute][$j + 1],
                        'Ошибка, проверьте правильность внесения: '.$this->getAttributeLabel(
                            $rules_array_sum[$attribute][$j + 1]
                        ).';'
                    );
                }
            }
            break;
        case '>=':
            if ((int)$this->$attribute < (int)$sum) {
                $this->addError(
                    $attribute,
                    'У Вас ошибка по '.$rules_array_sum[$attribute][0].' выделенных строк;'
                );
                for (
                    $j = 0, $count_info = count(
                        $rules_array_sum[$attribute]
                    ) - 1; $count_info > 0; $count_info--, $j++
                ) {
                    $this->addError(
                        $rules_array_sum[$attribute][$j + 1],
                        'Ошибка, проверьте правильность внесения: '.$this->getAttributeLabel(
                            $rules_array_sum[$attribute][$j + 1]
                        ).';'
                    );
                }
            }
            break;
    }
}
```
14. Применение & символа в фнукции 
```
public function actionRequestVisitorPrice() {
    $error_message = '';
    if($model->validate(Yii::$app->request->post()['MODELS']['name'], $error_message)){
        .....
    }
}
public static function validate($name, &$error_message = null, &$error_code = null) {
    $error_message = 'текст ошибки который вернуть';
}
```
