# JS-8

Кеша часто получает различного рода письма, и полезной информации в них не так много, как хотелось бы!

Ваша задача написать функцию `getUsefulInfo`, которая принимает список писем в формате:

```js
const letters = [
  {
    topic: '...',
    message: '...',
  },
  {
    topic: '...',
    message: '...',
  },
];
```

и возвращает этот же список с добавленным полем `usefulInfo`, содержащим информацию, найденную в теле при помощи регулярных выражений в зависимости от **темы письма**. Если информация не найдена, то `usefulInfo` будет равно `null`.

Кешу интересуют только определенные виды писем:

1. Если в **теме** письма содержится слово "**Встреча**", то в теле обязательно будет дата встречи в формате `dd.mm.yyyy HH:mm`. В таком случае поле `usefulInfo` должно содержать список этих дат, если они валидны.

```
01 <= dd <= 31
01 <= mm <= 12
00 <= HH <= 23
00 <= mm <= 59
```

```js
const letter = {
  topic: 'Встреча по обсуждению котиков',
  message: `
    С другой стороны дальнейшее развитие различных форм деятельности способствует подготовки и реализации систем массового участия. Равным образом сложившаяся структура организации обеспечивает широкому кругу (специалистов) участие в формировании системы обучения кадров, соответствует насущным потребностям.
    
    Какая то странная дата 32.13.9000 12:71
    Дата обзорной встречи назначена на 11.05.2022 22:11
    Дата встречи по итогам 13.05.2022 21:03
  `,
  usefulInfo: ['11.05.2022 22:11', '13.05.2022 21:03'],
};
```

2. Если в **теме** письма содержится слово "**компания**", то в теле обязательно содержится полное наименование компании в формате `*правовая форма* "Название организации"`, например `АО "Рыбу продаете"`.

```js
const letter = {
  topic: 'Обанкротилась еще одна компания',
  message: `
    Идейные соображения высшего порядка, а также перспективное планирование не оставляет шанса для своевременного выполнения сверхзадачи. С учётом сложившейся международной обстановки, дальнейшее развитие различных форм деятельности требует от нас анализа кластеризации усилий. Повседневная практика показывает, что современная методология разработки предопределяет высокую востребованность распределения внутренних резервов и ресурсов.
    Таким образом ООО "Очередная компания" постигла таже участь.
  `,
  usefulInfo: 'ООО "Очередная компания"',
};
```

3. Если в **теме** письма содержится слово "**автомобиль**, то в теле обязательно содержится номер автомобиля в формате `А356ОР 96`. Номер региона может содержать от двух до трех цифр, а буквы содержатся как в кириллице, так и в латинице. В таком случае поле `usefulInfo` должно содержать первый валидный номер.

```js
const letter = {
  topic: 'Вам назначен автомобиль',
  message: `
    Равным образом реализация намеченных плановых заданий позволяет оценить значение направлений прогрессивного развития. 
    По запросу Й657ОЯ 1024.
    Товарищи! сложившаяся структура организации обеспечивает широкому кругу (специалистов) участие в формировании позиций, занимаемых участниками в отношении поставленных задач.
    Номер автомобиля А457ОР 102.
    Таким образом реализация намеченных плановых заданий требуют определения и уточнения соответствующий условий активизации.
  `,
  usefulInfo: 'А356ОР 102',
};
```

4. ⭐ Если в **теме** письма содержится слово "**оплата**", то в теле обязательно будет сумма оплаты в формате `1,000.50 р.` или `100 р.`. В таком случае поле `usefulInfo` должно содержать первую найденную сумму, привиденную к числу.

```js
const letter = {
  topic: 'Требуется оплата по поручению №1337',
  message: `
    Идейные соображения высшего порядка, а также рамки и место обучения кадров представляет собой интересный эксперимент проверки соответствующий условий активизации. Сумма к оплате 1,000,000.35 р.
    Значимость этих проблем настолько очевидна, что сложившаяся структура организации играет важную роль в формировании новых предложений.
  `,
  usefulInfo: 1000000.35,
};
```
