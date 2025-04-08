# Лабораторная работа №2

**Тема:** Работа с предобученными моделями и эмбеддингами  
**Цель:** Научиться использовать предобученные трансформеры и исследовать влияние различных слоев модели.

**Студенты:** Чупахина В.В., Фомичева П.Ю.

---

## Содержание

1. [Теоретическая часть](#теоретическая-часть)  
2. [Описание разработанной системы (алгоритмы, принципы работы, архитектура)](#описание-разработанной-системы-алгоритмы-принципы-работы-архитектура)
3. [Результаты](#результаты)  
4. [Выводы](#выводы)  
5. [Список использованных источников](#список-использованных-источников)  

---

## Теоретическая часть

### Архитектура трансформера

Трансформер — архитектура глубоких нейронных сетей, представленная в 2017 году исследователями из Google Brain.

По аналогии с рекуррентными нейронными сетями (РНС) трансформеры предназначены для обработки последовательностей, таких как текст на естественном языке, и решения таких задач как машинный перевод и автоматическое реферирование. В отличие от РНС, трансформеры не требуют обработки последовательностей по порядку. Например, если входные данные — это текст, то трансформеру не требуется обрабатывать конец текста после обработки его начала. Благодаря этому трансформеры распараллеливаются легче чем РНС и могут быть быстрее обучены[1].

Архитектура трансформера (рисунок 1) состоит из кодировщика и декодировщика. Кодировщик получает на вход векторизованую последовательность с позиционной информацией. Декодировщик получает на вход часть этой последовательности и выход кодировщика. Кодировщик и декодировщик состоят из слоев. Слои кодировщика последовательно передают результат следующему слою в качестве его входа. Слои декодировщика последовательно передают результат следующему слою вместе с результатом кодировщика в качестве его входа.

Каждый кодировщик (рисунок 2) состоит из механизма самовнимания (вход из предыдущего слоя) и нейронной сети с прямой связью (вход из механизма самовнимания). Каждый декодировщик (рисунок 3) состоит из механизма самовнимания (вход из предыдущего слоя), механизма внимания к результатам кодирования (вход из механизма самовнимания и кодировщика) и нейронной сети с прямой связью (вход из механизма внимания) [1].

<p align="center">  
  <img src="https://upload.wikimedia.org/wikipedia/commons/0/0d/MLTransformerOverview.svg">
</p>

<p align="center">  
Рисунок 1 - Архитектура трансформера
</p>

<p align="center">  
  <img src="https://github.com/user-attachments/assets/50db7e21-d1ea-4098-856e-0bab8423df54">
</p>

<p align="center">  
Рисунок 2 - Кодировщик
</p>

<p align="center">  
    <img src="https://github.com/user-attachments/assets/06d4d53a-481d-4634-b68a-b8bf02753732">
</p>

<p align="center">  
Рисунок 3 - Декодировщик
</p>

Прежде чем подать данные в трансформер, нужно сначала преобразовать их в последовательность токенов — набор целых чисел, представляющих входные данные.
В нём слова должны быть сопоставлены с числами. Можно зарезервировать определенное число для представления любого слова, которого нет в словаре, поэтому мы сможем всегда оперировать целыми числами [2].

---

### Эмбеддинг

В широком смысле, эмбеддинг - это процесс преобразования каких-либо данных (чаще всего текста, но могут быть и изображения, звуки и т.д.) в набор чисел, векторы, которые машина может не только хранить, но и с которыми она может работать.
Эмбеддинг - это способ преобразования чего-то абстрактного, например слов или изображений в набор чисел и векторов. Эти числа не случайны; они стараются отражают суть или семантику нашего исходного объекта.

В NLP, например, эмбеддинги слов используются для того, чтобы компьютер мог понять, что слова «кошка» и «котенок» связаны между собой ближе, чем, скажем, «кошка» и «окошко». Это достигается путем присвоения словам векторов, которые отражают их значение и контекстное использование в языке.

Эмбеддинги не ограничиваются только словами. В компьютерном зрении, например, можно использовать их для преобразования изображений в вектора, чтобы машина могла понять и различать изображения [3].

**Векторные пространства** — это математические структуры, состоящие из векторов. Векторы можно понимать как точки в некотором пространстве, которые обладают направлением и величиной. В эмбеддингах, каждый вектор представляет собой уникальное представление объекта, преобразованное в числовую форму.

**Размерность вектора** определяет, сколько координат используется для описания каждого вектора в пространстве. В эмбеддингах высокая размерность может означать более детализированное представление данных. Векторное пространство для текстовых эмбеддингов может иметь тысячи измерений.

**Расстояние между векторами** в эмбеддингах измеряется с помощью метрик, таких как Евклидово расстояние или косинусное сходство. Метрики позволяют оценить, насколько близко или далеко друг от друга находятся различные объекты в векторном пространстве, что является основой для многих алгоритмов машинного обучения, таких как классификация

**В общем виде, эмбеддинги делятся на [3]:**

| Категория  | Тип | Описание |
| ------------- | ------------- | ------------- |
| Текстовые эмбеддинги  | Word Embeddings  | Эти эмбеддинги преобразуют слова в векторы, так что слова с похожим значением имеют похожие векторные представления. Они впервые позволили машинам понять семантику человеческих слов.  |
| Текстовые эмбеддинги  | Sentence Embeddings  | Здесь уже идет дело о целых предложениях. Подобные модели создают векторные представления для целых предложений или даже абзацев, улавливая гораздо более тонкие нюансы языка.  |
| Эмбеддинги изображений  | CNN  | CNN позволяет преобразовать изображения в векторы, которые затем используются для различных задач, например, классификации изображений или даже генерации новых изображений.  |
| Эмбеддинги изображений  | Autoencoders  | Автоэнкодеры могут сжимать изображения в более мелкие, плотные векторные представления, которые затем могут быть использованы для различных целей, включая декомпрессию или даже обнаружение аномалий.  |
| Эмбеддинги для других типов данных  | Graph Embeddings  | Применяются для работы с графовыми структурами (к примеру рекомендательные системы). Это способ представить узлы и связи графа в виде векторов.  |
| Эмбеддинги для других типов данных  | Sequence Embeddings  | Используются для анализа последовательностей, например, во временных рядах или в музыке.  |


### Модель RoBERTa

**RoBERTa** (*Robustly Optimized BERT Pretraining Approach*) — это модифицированная и улучшенная версия модели BERT, представленная исследователями из Facebook AI [2].

Ключевые отличия от BERT:
- Обучение на существенно большем объёме данных.
- Исключение задачи Next Sentence Prediction.
- Использование динамического маскирования токенов при обучении.
- Увеличенное время и объём предобучения.

Эти изменения делают RoBERTa более точной и устойчивой моделью для задач обработки естественного языка.

---



---
## Описание разработанной системы (алгоритмы, принципы работы, архитектура)

## Результаты

## Выводы

## Список использованных источников

1.  Википедия : сайт - URL: https://ru.wikipedia.org/wiki/%D0%A2%D1%80%D0%B0%D0%BD%D1%81%D1%84%D0%BE%D1%80%D0%BC%D0%B5%D1%80_(%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C_%D0%BC%D0%B0%D1%88%D0%B8%D0%BD%D0%BD%D0%BE%D0%B3%D0%BE_%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D1%8F) (дата обращения: 08.04.2025).

2. Habr : сайт - URL: https://habr.com/ru/companies/mws/articles/770202/ (дата обращения: 08.04.2025).
   
3. Habr : сайт - URL: https://habr.com/ru/companies/otus/articles/787116/ (дата обращения: 08.04.2025).

