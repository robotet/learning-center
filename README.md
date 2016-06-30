# Учебный центр по созданию децентрализованных автономных организаций на платформе Ethereum
В данном документе содержаться основные учебные уроки по созданию собственной децентрализованной автономной организации (далее сокр. ДАО) (1) с использованием автономных контрактов (2) из репозитория [Aira core](https://github.com/airalab/core).

## Урок 0: подготовьтесь к работе с сетью Ethereum через консоль.
Уровень сложности урока: низкий.

Вам необходим клиент сети Ethereum, поддерживающий работу в консольном режиме. Рекомендуется использовать клиент сети [geth](https://github.com/ethereum/go-ethereum#automated-development-builds) или [parity](https://ethcore.io/parity.html).

После установки клиента сети необходимо выполнить синхронизацию с **тестовой сетью**. После синхронизации с сетью необходимо добыть крайне небольшую сумму токенов для отправки транзакции, требуемой для выполнения первого урока. Сделать это можно одним из следующих способов:
- **Самый простой способ.** Мы создали [бесплатную раздачу 0,01 эфира на сайте aira.life](http://aira.life/tap/). Необходимо указать адрес аккаунта в тестовой сети и нажать кнопку "Send 0.01 ether". В течении ~ минуты данная сумма будет зачислена на баланс указанного аккаунта.
- **Чтобы познакомитсья с майнингом поближе.** следуя [инструкциям в официальной документации Ethereum](http://www.ethdocs.org/en/latest/mining.html#using-geth) включить майнинг в тестовой сети примерно на 20 - 30 минут.
- **Чтобы познакомитсья с Airalab поближе.** подключиться к каналу команды Airalab в Gitter: [Aira team friends](https://gitter.im/airalab/friends) и написать свой адрес в тестовой сети. Кто нибудь обязательно вам поможет!  

Добыв или получив от команды Airalab немного эфиров для первой транзакции в сеть можно обратиться к контракту Airalab в тестовой сети, который отправит вам в ответ **5 эфиров**, которых будет достаточно для выполнения всех 12 уроков.

### Пример выполнения
- TO DO: Eugene с Ethereum wallet
- [Пример выполнения урока с geth](https://github.com/airalab/learning-center/blob/master/lessons%20passage.md#%D1%83%D1%80%D0%BE%D0%BA-0)

## Урок 1: создайте ядро децентрализованной автономной организации.
Уровень сложности урока: низкий.

Ядро ДАО позволяет хранить реестр всех используемых организацией автономных контрактов. Для управления данным реестром (внесения/изменения/удаления записей) совместно с ядром необходимо создать контракт, который будет хранить реестр акционеров организации.

Для того, чтобы создать ядро и токен акций существует 2 варианта.

### Вариант 1: выполнить компиляцию исходного кода контрактов

Необходимы следующие контракты:
- [Core.sol](https://github.com/airalab/core/blob/master/sol/dao/Core.sol)
- [TokenEmission.sol](https://github.com/airalab/core/blob/master/sol/token/TokenEmission.sol)

> Обратите внимание, что вам требуется собрать все дополнительные контракты, которые используются ядром и реестром акционеров.

### Вариант 2: обратиться к фабрике ДАО отправив транзакцию со своего аккаунта к сборщику ядра [BuilderDAO](https://github.com/airalab/core/wiki/API-Reference#builderdao) следующего формата:

```js
var factory = eth.contract(Core).at("0x4b94c11ff4b118cad6d0d1831ecb60586a9241df")
var builder = eth.contract(BuilderDAO).at(factory.getModule("Aira BuilderDAO"))
builder.create(_dao_name, _dao_description, _shares_name, _shares_symbol, _shares_count,
               {from: eth.accounts[0], gas: 1000000, value: builder.buildingCost()})
```

#### Входные параметры

Параметр | Описание | Пример
---------|----------|-------
`_dao_name` | Название вашей организации | "Martian colony"
`_dao_description` | Краткое описание | "DAO for first human colony on Mars"
`_shares_name` | Название акций | Mars colony shares
`_shares_symbol` | Символ для акций, обычно 1 - 3 символа | MRS
`_shares_count` | Количество акций, эмиссируемых при создании ДАО | 10000


**Чтобы успешно выполнить данный урок необходимо:**
- обратиться к контракту `Lesson 1` для вызова функции `Execute()` указав `адрес контракта ядра ДАО`.

> Успешное выполнение урока в официальной сети даст: 50 `air`

#### Пример выполнения
- TO DO: Eugene с Ethereum wallet
- [Пример выполнения урока с geth](https://github.com/airalab/learning-center/blob/master/lessons%20passage.md#%D1%83%D1%80%D0%BE%D0%BA-1)

## Урок 2: Распределите акции вашей организации
Уровень сложности урока: низкий.

При создании ДАО на баланс адреса создателя было эмисировано заданное количество акций. Теперь время их распределить среди команды. Для того, чтобы это сделать можно использовать также клиент сети Ethereum wallet с GUI. Чтобы успешно выполнить данный урок необходимо разрешить снятие  1 акции адресу `Airalab learning center` и обратиться к контракту `Lesson 2` для вызова функции `Execute()`.

> Успешное выполнение урока в официальной сети даст: 50 `air`

#### Пример выполнения
- TO DO: Eugene с Ethereum wallet
- [Пример выполнения урока с geth](https://github.com/airalab/learning-center/blob/master/lessons%20passage.md#%D1%83%D1%80%D0%BE%D0%BA-2)

## Урок 3: Используйте общий контракт для хранения эфиров.
Уровень сложности урока: низкий.

Первый шаг к объединению средств организации от акционеров можно выделить в использование общего контракта, на который акционеры передадут средства без учета соотношения вложений к общей сумме средств в эфирах на общем контракте хранения эфиров. Это означает, что все средства, которые будут переведены на контракт будут доступны для использования и вывода **только** владельцу аккаунта, с которого средства были отправлены на контракт.

**Чтобы успешно выполнить данный урок необходимо:**
- обратиться к контракту [BuilderTokenEther](https://github.com/airalab/core/wiki/API-Reference#buildertokenether) в DAO factory с названием `Aira BuilderTokenEther` (`0xbb2695e90d82c6e4b87da5db29a6762645c7d6f5`) для создания контракта, который будет хранить эфиры.
- перевести **0,1** эфир на свой счет в контракте [TokenEther](https://github.com/airalab/core/wiki/API-Reference#tokenether), созданном вами ранее.
- обратиться к контракту `Lesson 3` для вызова функции `Execute()` указав `адрес контракта для хранения эфиров` и  имея **0,1** эфир на счету своего аккаунта на контракте.

> Успешное выполнение урока в официальной сети даст: 50 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- [Пример выполнения урока с geth](https://github.com/airalab/learning-center/blob/master/lessons%20passage.md#%D1%83%D1%80%D0%BE%D0%BA-3)

## Урок 4: Превратите акции ДАО в управленческий капитал фонда организации.

Уровень сложности урока: средний.

Теперь вам необходим модуль [Cashflow](https://github.com/airalab/core/wiki/API-Reference#cashflow) для дальнейшего управления средствами  в совместном финасировании расходов организации с использованием `пропорционального голосования` (3).

>Пропорциональное голосование выбрано, как начальная форма управления общим фондов организации в силу её наибольшей защищенности от влияния расходования средств отдельного акционера в общем бюджете организации.

Имея общий бюджет и модуль ДАО [CashFlow](https://github.com/airalab/core/wiki/API-Reference#cashflow) можно создавать [proposal](https://github.com/airalab/core/wiki/API-Reference#proposal) указывая:
- `Адрес в сети Ethereum - цель финансирования`.
- Запрашиваемое финансирования, меньшее чем общая сумма средств на счету `Cashflow`.

Чтобы успешно выполнить данный урок необходимо обратиться к контракту `Lesson 5` для вызова функции `Execute()` указав `адрес контракта получивший успешно финансирование от ДАО` и сумму в эфирах, которую получил контракт.

> Успешное выполнение урока в официальной сети даст: 100 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- [Пример выполнения урока с geth](https://github.com/airalab/learning-center/blob/master/lessons%20passage.md#%D1%83%D1%80%D0%BE%D0%BA-5)

## Урок 5: Эмиссируйте новые акции лично привлекая финансирование в эфирах.
Уровень сложности урока: средний.

Создатель ДАО на данном этапе может лично эмиссировать дополнительные акции на свой счёт. Это может быть полезно в том, случаи если к примеру основатель лично договорился с первым(ыми) инвесторами о вхождении их в состав акционеров за счёт привлечения финансирования с их стороны. Чтобы выполнить данный процесс безопасно для обеих сторон можно обратиться к `DAO factory` и найти сборщик с названием `Shares sale contract`.

**При обращении к сборщику необходимо указать:**
- адрес реестра, хранящего токены акций
- количество акций, которые продаются этим контрактом
- адрес реестра, хранящего эфиры
- количество эфиров требуемых для завершения сделки.

**После создания контракта `Shares sale contract` необходимо:**
- Отправить на адрес контракта `Shares sale contract` количество акций предлагаемых для продажи по контракту.
- Отправить на адрес контракта `Shares sale contract` количество эфиров, требуемое для сделки.

> Важно: акции поступят на баланс адреса, который отправил на контракт `Shares sale contract` не забывайте это. Эфиры, которые будут получены по данному контракту попадут на счёт адреса контракта `Cashflow`.

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с Ethereum wallet

## Урок 6: Создайте внутренний рынок ДАО
Уровень сложности урока: средний.

Создайте рынок ДАО и наполните его предложениями. Для начала необходимо обратиться к сборщику DAO factory [BuilderMarket](https://github.com/airalab/core/wiki/API-Reference#buildermarket), адрес в тестовой сети: `0xf2d826e8b8d36b85d6698ff99a8295e715304c48`.

`Aira BuilderMarket` создаст рынок [Market](https://github.com/airalab/core/wiki/API-Reference#market), на котором возможно выставлять на продажу токены.

Для того, чтобы познакомиться с работой на рынке давайте создадим 2 лота:
- лот на продажу **1 000 shares** организации за **500 credits**;
- лот на покупку **500 credits** за **1 эфир**;

TO DO: Eugene примеры запросов на добавление лотов на рынке (полная инструкция с всеми необходимыми шагами)

Чтобы успешно выполнить данный урок необходимо обратиться к контракту `Lesson 6` для вызова функции `Execute()` указав `адрес рынка`.

> Важно: на вашем рынке должны быть минимум 2 лота.

TO DO: vol4tim проверяй без учета активен или нет лот и того, что именно продаётся, главное наличие 2 лотов на рынке.

> Успешное выполнение урока в официальной сети даст: 100 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с geth

## Урок 7: Добавьте регулятора внутреннего рынка ДАО
Уровень сложности урока: средний.

Контракты типа `MarketRegulator` получают от рынка информацию о всех сделках проходящих на рынке, а также лотах, которые добавляют на рынок агенты. В данном уроке мы создадим регулятора рынка, который будет разрешать добавление лотов только с токенами, находящимися в реестре ядра ДАО.

TO DO: akru создания регулятора, связанного с реестром ядра ДАО.

**Для того, чтобы  включить регулятора в работу рынка необходимо:**
- обратиться в `DAO factory` к контракту `Market regulator builder` указав `DAO core address`.
- обратиться с аккаунта создателя рынка `owner` к контракту `DAO market`, для вызова функции `regulator_switch`, передав адрес, созданного регулятора.

**После добавления регулятора рынка можно попробовать его в работе. Для этого необходимо:**
- обратиться  в `DAO factory` к контракту `Token Emission Builder` для создания нового токена, который будет отражать ценность на вашем рынке.
- попробуйте добавить лот с любым количеством токенов на рынок - вы должны будете получить сообщение следующего формата: "Данный токен не найден в реестре ядра ДАО".
- добавьте токен в реестр ядра ДАО.
- попробуйте снова добавить лот с любым количеством токенов на рынок - лот должен добавиться.

TO DO: akru прочитай логику, думаю, что есть что ещё доработать в контрактах для реализации данных шагов.

> Совет: например в DAO Aira на внутреннем рынке есть предложение токенов кураторства команды Aira для вашей DAO. 1 токен = 1 месяцу поддержки. Придумайте такой токен, который был бы полезен в дальнейшем в работе.

Для прохождения данного урока, необходимо обратиться к контракту `Lesson 7`, для вызова функции `Execute()` указав `адрес рынка`.

> Успешное выполнение урока в официальной сети даст: 100 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с geth

## Урок 8: Добавьте первого агента рынка
Уровень сложности урока: средний.

Добавленный на предыдущем шаге регулятор выполняет не только функцию фильтрации предлагаемых на рынок ДАО ценностей, но также помагает выполнять свои задачи контрактам агента рынка. Контракты типа `MarketAgent` позволяют строить логику работы автономного агента с рынком без участия человека. В данном примере мы создадим самого простого агента, который будет автоматически выставлять на рынок все токены, которые будут разрешены для снятия контракту агента рынка, а также при покупке данных токенов на рынке за внутреннюю валюту `credits`, выполнять поиск покупателей `credits` для продажи их за эфиры. Тем самым автономный агент, желающий предложить свою ценность на внутреннем рынке ДАО, сможет сразу получать эфиры.

**Для того, чтобы  включить агента рынка в работу ДАО необходимо:**
- обратиться к `DAO factory` и найти контракт сборщика с названием `Market agent ether out`, при обращении к данному сборщику необходимо указать адрес токена ценности, которую вы хотите продавать на внутреннем рынке ДАО, а также адрес рынка. Советуем использовать токен, который был создан ранее в уроке 7.
- внести в реестр агентов рынка в контракте `Market regulator`, созданный контракт агента.

TO DO: akru создать билдер и написать пример обращения к билдеру с указанием данных для конструктора.

Для прохождения данного урока, необходимо обратиться к контракту `Lesson 8`, для вызова функции `Execute()` указав `адрес контракта агента` и `адрес контракта рынка`.

> Успешное выполнение урока в официальной сети даст: 100 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с geth

## Урок 9: Добавьте регулятора эмиссии кредитов.
Уровень сложности урока: высокий.

На данный момент `owner`, создавший контракт токенов `credit` может бесконтрольно выполнять эмиссию новых токенов на свой баланс. Это помешает развитию вашего рынка и повышения ценности вашей внутренней валюты ДАО. Для того, чтобы решить данную проблему в данном уроке будет создан регулятор эмиссии токенов `credit` и внедрён в работу рынка с помощью голосования акционеров.

**Для того, чтобы внедрить регулятора эмиссии кредитов необходимо:**
- Обратиться к `DAO factory` и найти контракт сборщика с названием `Emission regulator via Market trade`, при обращении к данному сборщику необходимо указать `адрес токена внутренней валюты ДАО`, `адрес, на который будет происходить эмиссия новый токенов`, а также `процент эмиссируемых новых токенов`. В данном уроке, можно указать адрес, на который будет производиться эмиссия - адрес основателя DAO. В дальнейшем этом адрес может сменить `owner` контракта `Emission regulator via Market trade`.
- Добавть в реестр ядра новую запись с указанием `адреса контракта регулятора эмиссии` и названием `Credits emission regulator via Market trade`.
- Обратиться к контракту `Credits ledger` от аккаунта `owner` для смены адреса владельца на адрес контракта `Emission regulator via Market trade`.
- Обратиться к контракту `DAO market` вызвав функцию `AddMarketWatcher()`, указав адрес контракта `Emission regulator via Market trade` и тип событий `Deal`.

**Для того, чтобы проверить работу регулятора эмиссии:**
- Выполните любую сделку на рынке.
- Обратитесь к контракту `Credit ledger` и проверьте, что заданая вами сумма эмиссия в процентрах от сделки была эмиссирована на счет основателя DAO.

**Для того, чтобы успешно пройти урок необходимо:**
- обратиться к контракту `Lesson 9`, для вызова функции `Execute()` указав `адрес контракта рынка`.

> Успешное выполнение урока в официальной сети даст: 200 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с geth

## Урок 10: Увеличивайте ликвидность ваших внутренних токенов ДАО (кредитов)
Уровень сложности урока:  средний.

Помните, что главная задача любой организации - это создавать ценность для мира. Еще лучше если эта ценность будет ликвидна на внешних рынках. Ценность вашей организации теперь отражается внутренним токеном, а значит чем активнее рынок ДАО, чем больше сделок и больше интересных предложений на внутреннем рынке, тем ценнее токен, за который можно приобрести данные ценности.

**Для того, чтобы увеличить ликвидность кредитов вашей ДАО необходимо:**
- Инвестировать в создание новых ценностей, которые будут полезны на внутреннем рынке ДАО.
- Увеличивать активность агентов рынка. Создавайте новых агентов рынка, которые способны автоматически приобретать токены на рынке, при продаже своей продукции/услуг.
- Привлечь новых агентов рынка в вашем ДАО.

**Для того, чтобы успешно пройти урок необходимо:**
- обратиться к контракту `Lesson 10`, для вызова функции `Execute()` указав `адрес контракта рынка`. Обратите внимание, что вам необходимо, чтобы на рынке было минимум **5 активных** предложений покупки/продажи  на **разные** ценности.

> Успешное выполнение урока в официальной сети даст: 100 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с geth

## Урок 11: Назначьте совет директоров организации
Уровень сложности урока:  высокий.

На данный момент ваша организация всё еще управляется всеми акционерами. Т.е. каждый акционер самостоятельно принимает решение об инвестровании средств пропорциональных его управленческому капиталу (количеству акций) в тот или иной запрос инвестирования. С ростом организации и количества акционеров необходимо изменять схему управление для внедрения избираемого совета директоров.

**Для того, чтобы внедрить совет директоров в работу организации необходимо:**
- Обратиться к `DAO factory` и найти контракт сборщика с названием `Board of Directors builder`, при обращении к данному сборщику необходимо указать адрес реестра акционеров (токенов акций), форму голосования `majority` (простое большинство, 51%) и адрес токена, хранящего капитал организации.
- Создав контракт совета директоров необходимо раздать токены голосов, тем самым составить список членов совета директоров.
- Проголосовать как минимум 51% всех токенов акций за активирование токена совета директоров `electBoardofDirectors()`.
- Указать владельцем контракта, хранящего капитал организации контракт совета директоров.

> В контракте совета директоров можно создавать голосования по вопросу смены совета директоров, если в каком либо голосовании набирается 51% голосов, то управление переходит новому реестру участников совета. Акционеры не могут голосовать за несколько вариантов совета одновременно. Голосование замораживает акции акционера, акционер всегода может забрать свой голос, тем самым разморозить свои акции.

**Для того, чтобы попробовать работу совета директоров необходимо:**
- Создать запрос на финансирование `proposal` от любого из членов совета директоров.
- Провести встречу совета директоров и проголосовать за запрос финансорования, так чтобы набралось 51% голосов.
- Проверить поступление средств на счёт `target`.

**Для того, чтобы успешно пройти урок необходимо:**
- обратиться к контракту `Lesson 11`, для вызова функции `Execute()` указав `адрес контракта совета директоров`. Обратите внимание, что вам необходимо, чтобы совет директоров проголосовал и одобрил хотя бы за **1** запрос финансорования.

> Успешное выполнение урока в официальной сети даст: 200 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с geth

## Урок 12: Crowdsale
Уровень сложности урока: высокий.

Помните самая важная задача организации - повышать ликвидность своей внутренней валюты, насыщая рынок ДАО предложениями. Для стимулирования рынка необходимо инвестировать в поставщиков ценностей рынка ДАО, а для этого необходимы существенные финансовые средства. Для того, чтобы привлечь дополнительные капиталы давайте выполним эмиссию и продажу по фиксированной цене акций организации - crowdsale.

**Для того, чтобы выполнить crowdsale необходимо:**
- Обратиться к `DAO factory` и найти контракт сборщика с названием `Crowdsale builder`, при обращении к данному сборщику необходимо указать адрес реестра, хранящего токены акций, а также адрес реестра, хранящего капитал организации в эфирах.

Для увеличения количества акций за счёт привлечения финансирования необходимо воспользоваться сборщиком [BuilderCrowdsale](https://github.com/airalab/core/wiki/API-Reference#builderipostart), который создаст модуль инфраструктуры ДАО [Crowdsale](https://github.com/airalab/core/wiki/API-Reference#ipo).

**Параметры, которые необходимо задать при обращении к сборщику `Crowdsale`:**
- Адрес токена кредитов
- Адрес токена акций
- Время старта Crowdsale (UNIX-время)
- Период проведения Crowdsale в секундах
- Начальная стоимость акций
- Шаг увеличения стоимости в процентах
- Период шага увеличения стоимости в секундах
- Минимальную сумму привлекаемых средств
- Максимальную сумму привлекаемых средств

> в данном уроке максимальную сумму привлекаемых средств необходимо указать равной 5 эфиров.

*Внимание*: После создания контракта на его адрес необходимо перевести число акций для продажи.

Для успешного прохождения урока необходимо внести 5 эфиров с любого аккаунта, который в дальнейшем станет владельцем новых акций и будет участвовать в управлении расходами вместе с уже имеющимися акционерами. Чтобы закончить урок необходимо отправить транзакцию после наполнения Crowdsale 5 эфирами на `Lesson 12` вызвав функцию `Execute()`.

> Успешное выполнение урока в официальной сети даст: 200 `air`

#### Пример выполнения
- TO DO: Eugene пример с Ethereum wallet
- TO DO: vol4tim пример с geth
