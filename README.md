# FIFA-Analysis

В рамках данного проекта мы проводим исследование, посвященное анализу ценообразования карточек игроков на сайте https://www.futwiz.com/. Стоимость игрока (колонка "Price") определяется большим количеством различных параметром, часть из которых кажутся на первый взгляд совсем не важными. 

__Размер данных оказался слишком большим, поэтому вот [ссылка](https://drive.google.com/file/d/1bgt_r2R2AxXtI51iQW1prC80O3qJn3TY/view?usp=sharing) на гугл диск с данными__


Основные моменты проведенного исследования:
1) Игроки одной национальности или лиги дают друг другу улучшение характеристик в игре. А есть карточки которые априори имеют улучшенные характеристики (иконы). В связи с этим будем проверять, действительно ли лига и нация игрока влияет на его цену. Проверять это будем считая коэффициент корреляции Спирмена количества игроков в стране/лиге и средней их стоимости.
2) Если игрок поставлен играть на ту позицию, что у него на карте, то его характеристики улучшаются. При этом игроку можно поменять позицию, в зависимости от наличия и количества альтернативных позиций. Поэтому мы проверим гипотезу о том, что игроки, имеющие хотя бы одну альтернативную позицию стоят дороже, чем игроки, которые не имеют не одной. 
3) FIFA 23 - коммерческая игра, которая генерирует деньги засчет большого потока пользователей. Чтобы поддерживать интерес к игре на протяжении всего сезона, в игру добавляются почти каждую неделю новые карточки футболисты. При этом, для большей части футбольного сообщества главынй интерес представляют игроки и клубы, которые находятся в топ-5 лигах (английской, испанской, немецкой, французской и итальянской). Поэтому, во-первых, спрос на таких игроков должен быть больше, что значит, что и цены будут выше, но также это значит, что компания будет заинтересована добавлять игроков по большей части из описанной выше категории, поэтому и цениться они будут больше. Поэтому мы проверим гипотезу, что игроки из топ-5 лиг стоят дороже, чем игроки не из топ-5 лиг.
4) FIFA 23 - аркадная игра, в которой первоочередное внимание уделено динамичности и высоким скоростям, что делает обычно счета в матчах скорее хоккейными, нежели футбольными. Поэтому, кажется, что чем ближе игрок к линии атаки, тем дороже он должен стоить, ведь именно нападающие забиывают много красивых голов, и к тому же нападающие чаще более яркие и известные, чем игроки полузащиты и защиты. Поэтому мы проверим гипотезу о том, что линия расположения на поле (нападение, защита, полузащита) влияет на стоимость игрока.
5) FIFA 23 - это видеогра, и как и в любой видеоигре, здесь очень хорошо работают внутриигровые скрипты. Так, например, многие профессиональные игроки любят играть маленькими и быстрыми нападающими, нежели нападающими, у которых очень хорошие показатели удара или паса, просто потому что в данной игре скорость и дриблинг дают возможность забивать уйму голов, причем самым простыми способами, тогда как тяжёлыми, высокими нападающими играть крайне тяжело, несмотря на то, что их физические показатели лучше, чем у маленьких и быстрых. Поэтому мы выясним, действительно ли маленькие и быстрые нападющие стоят дороже, чем высокие и мощные.
6) Как уже упоминалось, в игре огромное количество различных "цветных" карточек. Поделим их на два вида: премиальные - обычные игроки, которые получили особую карточку, и кумиры - игроки, которые закончили с футболом, но прославились на множество десятков лет вперед. Интересно сравнить, отличаются ли в среднем цены на них или значительной разницы нет.
7) Наша задача заключается в предсказании стоимости игрока, поэтому мы выбираем регрессионные модели. Линейная регрессия кажется неприменимой в нашем случае в силу специфики распределения цен. Далее мы рассматривали различные модели градиентного бустинга (классический и CatBoostRegressor), подбирая число самых значимых признаков и гиперпараметры. 

Выводы по каждому пункту:
1) Мы изучили, коррелирует ли количество игроков в стране/лиге со средней ценой игрока. Коэффициенты корреляции Спирмена получились 0.6 и 0.3 для стран и лиг, соответственно. Поэтому можно утверждать, что вероятнее всего есть зависимость для стран, но для лиг это не так очевидно. Наше предположение оказалось частично верно.
2) С помощью z-теста, мы получили, что рассматривая все карточки, присутствует различие в цене между карточками, у которых нет альтернативных позиций и есть хотя бы одна. Однако это могло вызываться тем, что у игроков с очень низким рейтингом нет альтернативных позиций, а у игроков с высоким рейтингом, за очень маленьким исключением, есть хотя бы одна альтернативаю. Поэтому мы решили отдельно сравнить цены у игроков с самыми ходовыми рейтингами 75-82. И там оказалось, что наличие альтернативных позиций не влияет на цену игрока. Аналогичный результат наблюдался и для рейтингов 65-75. Глоабльно мы оказались правы, однако если рассматривать отдельно взятые когорты игроков, то вывод не такой однозначный
3) С помощью перестановочного теста мы заключили, что цены для игроков из топ-5 лиг больше чем для игроков не из топ-5 лиг. Однако мы также разбили выборки футболистов на 4 когорты: 83+, 75-82, 65-75 и <65. Мы полчили, что для 83+, 65-75 и <65 признак топ-5 лиг оказался значим, а для 75-82 оказался не значим. Как и в прошлом пункте, глобально мы оказались правы, но на отдельных выборках не во всех случаях.
4) C помощью обратного перцентильного бутстрапа мы построили 95% доверительные интервалы для каждой линии игроков на поле и получили, что они не пересекаются и более того, границы CI для нападающих больше границ CI для полузащитников, а у полузащитников больше, чем у защитников. Наше предположение оказалось полностью верно.  
5) С помощью z-теста, мы получили, что маленькие юркие футболисты стоят в среднем дороже, чем мощные высокие. Наше предположение оказалось верно
6) С помощью z-теста, мы получили, что иконы оказались дороже, чем премиальные игроки, интересный результат, но логичный. Иконы дают всей команде дополнительные улучшения, чего не могут сделать все остальные игроки.
7) градиентный бустинг дал следующие результаты: без отбора признаков MAE = 13437. Далее модель показала наилучшее качество при выборе 50 наиболее важных признаков, MAE = 10867. Модель CatBoostRegressor с 50 наиболее важными признаками дала результат MAE = 176444 (при этом на трейне было 2387, что значит, что модель переобучил). С помощью GridSearchCV мы подбирали гиперпараметры и получили MAE = _.  Как видим, лучшее качество показала модель ___. 
