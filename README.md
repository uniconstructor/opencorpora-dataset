# opencopora-dataset

Обучающая выборка текстов opencorpora.org для разбиения текста на предложения

Ссылка на дамп базы данных, на основе которого создана выборка: http://opencorpora.org/?page=downloads

## Структура папок

Каждая папка в датасете соответствует одной записи в таблице books. Имя - поле book_id.

Каждая папка хранит данные одного документа:
* <book_id>-sentences.csv - список всех предложений документа (разбиение составлено вручную)
* <book_id>-sentences-агещ.csv - список всех предложений документа (разбиение составленное автоматически, для baseline)
* <book_id>-text.txt - текст документа, составленный из предложений
* <book_id>-original.html - сохраненная копия веб-страницы из которой был извлечен текст (если есть)
* <book_id>-annotations.xml - полная разметка документа в формате opencopora. Описание формата можно посмотреть здесь: http://opencorpora.org/?page=export

### Структура csv-файла со списком предложений документа

* sent_id - уникальный id предложения в базе opencopora
* par_id - уникальный id абзаца текста в базе opencopora
* source - текст предложения
* book_id - id документа в котором находится предложение
* par_pos - порядковый номер абзаца текста, в котором находится это предложение. Абзацы нумеруются с 1, заголовок текста считается первым абзацем
* sent_pos - порядковый номер предложения внутри абзаца текста. Предложения нумеруются с 1.

## Обучающая выборка и предобученные модели для библиотеки sentencepiece

Для разбиения текста на предложения используется библиотека sentencepiece: https://github.com/google/sentencepiece

Документация по python-обертке: https://github.com/google/sentencepiece/blob/master/python/README.md

В корне проекта находится список файлов для нее:
* train.txt - обучающая выборка для токенизатора: предстваляет собой текстовый файл в котором собраны все предложения из базы opencopora (каждое предложение с новой строки)
* m.model - предобученная модель для разбиения текста на предложения
* m.vocab - словарь токенизатора sentencepiece (подробнее: https://github.com/google/sentencepiece#vocabulary-restriction)  и 
