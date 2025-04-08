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
![image](https://upload.wikimedia.org/wikipedia/commons/0/0d/MLTransformerOverview.svg)
</p>

<p align="center">  
Рисунок 1 - Архитектура трансформера
</p>

<p align="center">  
![image](https://github.com/user-attachments/assets/2b7780d2-a875-4283-9a50-6775ba069197)

</p>

<p align="center">  
Рисунок 2 - Кодировщик
</p>

<p align="center">  
![image](https://github.com/user-attachments/assets/cb4ab42a-fc65-4b92-98d3-d6701329f098)

</p>

<p align="center">  
Рисунок 3 - Декодировщик
</p>
---

### Модель RoBERTa

**RoBERTa** (*Robustly Optimized BERT Pretraining Approach*) — это модифицированная и улучшенная версия модели BERT, представленная исследователями из Facebook AI [2].

Ключевые отличия от BERT:
- Обучение на существенно большем объёме данных.
- Исключение задачи Next Sentence Prediction.
- Использование динамического маскирования токенов при обучении.
- Увеличенное время и объём предобучения.

Эти изменения делают RoBERTa более точной и устойчивой моделью для задач обработки естественного языка.

---

### Эмбеддинги в трансформерах

**Эмбеддинг** — это способ представления текста в виде плотных векторов фиксированной размерности. В трансформерах используется несколько видов эмбеддингов:

- **Token Embeddings** — представление слов или подслов.
- **Positional Embeddings** — добавляют информацию о позиции токена в последовательности.
- **Hidden States** — векторы, полученные на выходе каждого слоя трансформера.
- **[CLS] эмбеддинг** — вектор специального токена `[CLS]`, часто используемый для классификации текста как агрегированное представление всей последовательности.

---

### Поведение слоев трансформера

Исследования показывают, что различные слои трансформера специализируются на разных аспектах лингвистической информации:

- **Нижние слои** хорошо захватывают **морфологические и синтаксические** структуры.
- **Средние слои** содержат **семантическую** информацию.
- **Верхние слои** подстроены под задачу обучения (например, предсказание маскированных токенов) и могут быть менее универсальными [3][4].

---
## Описание разработанной системы (алгоритмы, принципы работы, архитектура)

## Результаты

## Выводы

## Список использованных источников

1.  Википедия : сайт - URL: https://ru.wikipedia.org/wiki/%D0%A2%D1%80%D0%B0%D0%BD%D1%81%D1%84%D0%BE%D1%80%D0%BC%D0%B5%D1%80_(%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C_%D0%BC%D0%B0%D1%88%D0%B8%D0%BD%D0%BD%D0%BE%D0%B3%D0%BE_%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D1%8F) (дата обращения: 08.04.2025).

