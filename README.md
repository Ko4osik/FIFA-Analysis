# FIFA-Analysis

В рамках данного проекта мы проводим исследование, посвященное анализу ценообразования карточек игроков на сайте https://www.futwiz.com/. Стоимость игрока (колонка "Price") определяется большим количеством различных параметром, часть из которых кажутся на первый взгляд совсем не важными. 

Также существует множество низкоуровневых причин ценообразования игроков, которые нельзя переложить в данные:
1) Игроки одной национальности или лиги дают друг другу улучшение характеристик в игре. А есть карточки которые априори имеют улучшенные характеристики (иконы). В связи с этим будем проверять, действительно ли лига и нация игрока влияет на его цену. Проверить это можно
2) 
3) Также в игре есть множество заданий и сборок игроков, которые предполагают использование игроков определенных лиг и национальностей. Соответственно цены на нужных игроков могут подниматься. Мы попробуем предугадать, какие футболисты требовались в момент парсинга данных и сравним с реальностью
4) ...

Для реализации проекта мы будем использовать методы машинного обучения и статистического анализа. Предварительно, мы соберем данные о карточках игроков с веб-сайта futwiz.com и проанализируем их, чтобы выявить возможные закономерности в ценообразовании. Затем мы приступим к обучению модели, которая будет предсказывать цену игроков на основе имеющихся данных. Вероятно, будет использован градиентный бустинг, который помогает откидывать параметры, которые имеют наибольшее влияние на цену. 

__Мы столкнулись с проблемой, что у нас слишком мало данных (всего 1500), поэтому в целях спарсить хотя бы 10к__
