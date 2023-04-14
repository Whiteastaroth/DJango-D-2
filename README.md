Список команд запускаемых в Django Shell (перед нами стоят задачи из 11 пунктов)


1. Создать двух пользователей (с помощью метода User.objects.create_user('username')). /при создании проекта, так же был создан superuser/
user1 = User.objects.create_user(username='Andrey') user2 = User.objects.create_user(username='Polina')


2.Создать два объекта модели Author, связанные с пользователями.
Author.objects.create(authorUser=user1) Author.objects.create(authorUser=user2)


3.Добавить 4 категории в модель Category.
Category.objects.create(name='Новости автозвука') Category.objects.create(name='Фестивали')
Category.objects.create(name='Рекомендации по выбору оборудования') Category.objects.create(name='Планируем бюджет')


4.Добавить 2 статьи и 1 новость.
author = Author.objects.get(id=1) Post.objects.create(author=author,
categoryType='NW', title='Apple Music войдет в стандартное оснащение Audi', 
text='Начиная с ближайшего времени мультимедийные системы в автомобилях Audi получат предустановленный Apple Music. Независимо от 
предпочтений будущего владельца приложение зашьют еще на заводе. Там, где это возможно, Apple Music появится в Audi с очередным обновлением прошивки.

author = Author.objects.get(id=2) Post.objects.create(author=author,
categoryType='AR', title='Календарь соревнований по Автозвуку 2023', text='Перед вами календарь соревнований по автозвуку, которые будут проводиться в России весной 2023.
Это планируемые даты, которые могут корректироваться. Информацию об изменениях сроков и подробности обязательно уточняйте по официальным ссылкам внизу страницы.

author = Author.objects.get(id=1) Post.objects.create(author=author,
categoryType='AR', title='Рекомендации по прослушке сабвуфера.', text='Конечно же, звук в помещении магазина будет сильно отличаться от звучания в салоне автомобиля.
Но как же приобрести устройство без его предварительного прослушивания? Основные рекомендации по прослушке: 1. Не стоит, конечно же, включать абсолютно каждый сабвуфер.
Достаточно остановиться на нескольких моделях, которые соответствуют требуемым техническим характеристикам, и прослушать именно эти сабвуферы. 
   2. Важно сравнивать звучание на разнообразных стилях музыки, в которых будет как высокий, так и низкий бас, помимо этого, медленный и быстрый темп. 
   3. Лучший вариант — это прослушать свои любимые музыкальные треки. 3. Важно выбрать одну точку для прослушки, поскольку в разных сторонах помещения звук может сильно разниться.
   4.  4. Не стоит забывать, что сабвуфер со временем может разыграться и его громкость, как и бас, станет более четким и быстрым. Конечно же, эти правила касаются только выбора сабвуфера в коробке.
   5.   Сравнивать параметры звучания сабвуферных динамиков нет никакого смысла.')


5.Присвоить им категории (как минимум в одной статье/новости должно быть не меньше 2 категорий).
Post.objects.get(id=1).postCategory.add(Category.objects.get(id=2)) Post.objects.get(id=2).postCategory.add(Category.objects.get(id=1))
Post.objects.get(id=3).postCategory.add(Category.objects.get(id=3), Category.objects.get(id=4))


6 Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий).
Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=1).authorUser, text='Делюс впечатлениями прошлого года, надеюсь этот будет не хуже. 
Ну сперва об организации! Ребята — это вышак! Организаторы пеклись о каждой мелочи! Это просто очень было заметно и предельно радовало! Конкурсы, призы, 
рассказы о студиях и компаниях партнеров — ничто не было оставлено без внимания! Больше всего поразило то, что с таким скромным бюджетом оргам удалось привезти на фестиваль саму Бритни Спирс!)))
География — Москва, Питер, Калуга, Рязань, Иваново, Владимир и вся Московская область, города которой перечислять наверное замучаюсь! Всем удачи')

Comment.objects.create(commentPost=Post.objects.get(id=2), commentUser=Author.objects.get(id=2).authorUser, text='А оно нам надо?:) Видимо менеджмент
VW не долго думая решил позаимствовать пример распространения альбома U2 "Songs Of Innocence". Только там вроде как он распространялся бесплатно. Может и AUDI раздавать будут, какое-то время, бесплатно? :)')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=2).authorUser, text='Даже не стоит тратить своих денег и времени на этот девайс. Место занимает, систему удорожает. Ресурс потребляет.')

Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=1).authorUser, text='Пожалуй,саб нужен для соревнований по автозвуку и для аудиофилов. 
Достаточно хорошик динамиков на зад и грамотную настройку усилка. Не забываем про процессорную голову.')


7.Применяя функции like() и dislike() к статьям/новостям и комментариям, скорректировать рейтинги этих объектов.
Comment.objects.get(id=1).dislike() Comment.objects.get(id=1).like() Comment.objects.get(id=1).dislike() Comment.objects.get(id=1).like() Comment.objects.get(id=1).like() Comment.objects.get(id=1).like()

Comment.objects.get(id=2).like() Comment.objects.get(id=2).like() Comment.objects.get(id=1).dislike()

Comment.objects.get(id=3).like() Comment.objects.get(id=3).dislike() Comment.objects.get(id=3).dislike() Comment.objects.get(id=3).like() Comment.objects.get(id=3).dislike()

Comment.objects.get(id=4).dislike() Comment.objects.get(id=4).dislike()

Post.objects.get(id=1).like() Post.objects.get(id=1).like() Post.objects.get(id=1).like() Post.objects.get(id=1).dislike()

Post.objects.get(id=1).like() Post.objects.get(id=1).like()

Post.objects.get(id=2).like() Post.objects.get(id=2).dislike() Post.objects.get(id=2).dislike()

Post.objects.get(id=3).like() Post.objects.get(id=3).dislike() Post.objects.get(id=3).like() Post.objects.get(id=3).like() Post.objects.get(id=3).dislike()

8.Обновить рейтинги пользователей.
author1 = Author.objects.get(id=1) author1.update_rating()

author2 = Author.objects.get(id=2) author2.update_rating()
9.Вывести username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта).
author = Author.objects.order_by('-ratingAuthor')[:1][0] author.authorUser.username author.ratingAuthor

10. Вывести дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье.
b =Post.objects.order_by('-rating')
>>> for i in b[:1]:
        i.categoryType
        i.author.ratingAuthor
        i.rating
        i.title
        i.preview()


11. Вывести все комментарии (дата, пользователь, рейтинг, текст) к этой статье.

Post.objects.all().order_by('-rating')[0].comment_set.values('dateCreation', 'commentUser', 'rating', 'text')
