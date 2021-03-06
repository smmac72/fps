# Богомолов Олег - and A Better Life
# Пользовательские сценарии

### Группа: 10МИ3
### Электронная почта: smmac072@gmail.com
### VK: https://vk.com/smmac72

### [ Сценарий 1 - Запуск игры ]
1. Пользователь открывает .exe файл игры
2. Открывается приложение и переключается в полноэкранный режим
3. В окне приложения показывается загрузочный экран, в это время загружаются необходимые для меню компоненты
4. После окончания загрузки показывается главное меню:
* Продолжить игру (при наличии SAVE-файла)
* Новая игра
* Настройки
* Выход
5. При выборе "Продолжить игру" запускается Сценарий 2
6. При выборе "Новая игра" запускается Сценарий 3
7. При выборе "Настройки" запускается Сценарий 4
8. При выборе "Выход" появляется окно "Вы желаете покинуть игру?". При выборе "Да" окно игры закрывается. При выборе "Нет" окно выбора закрывается

### [ Сценарий 2 - Продолжение игры ]
1. Идет проверка повреждений SAVE-файла. При их наличии выводится ошибка
2. Выбирается текущий уровень из SAVE-файла
3. Показывается катсцена, прикрепленная к началу уровня
4. Прогружаются необходимые для уровня файлы
5. Если загрузка кончилась до конца катсцены, появляется возможность ее пропустить
6. Если загрузка продолжается после конца катсцены, отображается черный экран
7. После катсцены/При ее пропуске рендерится карта, слева внизу отображаются данные в формате:
* Название задания
* Имя главного героя
* Место
* Дата
8. Запускается сценарий 5

### [ Сценарий 3 - Новая игра ]
1. Создается SAVE-файл игры. 
2. При его наличии появляется диалоговое окно с текстом: "Вы желаете перезаписать сохранение?". 
3. При выборе "Да" SAVE-файл перезаписывается. При выборе "Нет" диалоговое окно закрывается
4. В SAVE-файл записываются дефолтные данные, с которыми будет проводиться загрузка
5. Показывается вступительная катсцена, которую возможно пропустить
6. Запускается Сценарий 2 с новым SAVE-файлом

### [ Сценарий 4 - Настройки ]
1. Показывается меню:
* Игровой процесс
* Управление (привязка кнопок)
* Графика
* Звук
2. При выборе "Игровой процесс" показывается меню:
* Сложность - Легко/Нормально/Сложно
* Помощь в наведении - Выключить/Включить
* Настройка интерфейса 
3. При выборе "Управление" показывается меню:
* Передвижение
* Бой
* Действия
Все кнопки назначаются в меню
4. При выборе "Графика" показывается меню:
* Разрешение
* Качество текстур - Низкое/Среднее/Высокое/Ультра
* Качество теней - Низкое/Среднее/Высокое/Ультра
* Ограничение кадров - 30 FPS / 60 FPS / Нет ограничений
5. При выборе "Настройка интерфейса" возможно перетаскивать интерфейс и включать/выключать его необходимые компоненты
6. При выборе "Разрешения" будет измеряться разрешение экрана пользователя и выдавать все разрешения до его включительно

### [ Сценарий 5 - Выполнение миссии ]
1. В списке задач появляется основная задача этой миссии
2. Появляется второстепенная задача (или несколько)
3. При достижении задачи (близость к координатам, падение здоровья выбранного актера до 0) она объявляется выполненной
4. При выполнении второстепенной задачи может появиться новая второстепенная (в определенных случаях)
5. При выполнении основной задачи обязательно появляется новая основная задача, если она не является последней
6. При достижении последней основной задачи уровень завершается, экран затемняется и начинается загрузка нового уровня по Сценарию 2

### [ Сценарий 6 - Взаимодействие с оружием ]
1. При нажатии кнопки выстрела количество патронов в обойме уменьшается на 1
2. Проигрывается звуковой и визуальный эффекты. Создается объект гильзы (при необходимости), который падает на землю и производит звуковой эффект
3. Создается объект снаряда с изначальным вектором скорости
4. При столкновении снаряда с объектом его конечная скорость рассчитывается по текущей скорости снаряда, его углу попадания и коэффициенту пробиваемости (у каждого материала свой)
5. Объекту наносится урон. Для объекта запускается Сценарий 7
6. При слишком большом угле попадания (относительно перпендикуляра, опущенного на эту плоскость) происходит рикошет, и снаряд теряет часть скорости, отражаясь на 90 градусов
7. Если при попадании конечная скорость > 0, то снаряд пролетает через объект
8. Если при попадании конечная скорость <= 0, то снаряд не пролетает через объект
9. При нажатии кнопки прицела (если возможно) активируется режим прицеливания через прицел, установленный на оружии

### [ Сценарий 7 - Разрушаемость ]
1. Проверяется тип объекта: процедурно разрушаемый, обычный или неуничтожаемый
2. Если объект обычный, то если его здоровье меньше 0, то он уничтожается. Иначе на нем появляется декаль от выстрела, спецэффекты, соответствующие материалу, и объект отлетает согласно законам физики
3. Если объект неуничтожаемый, то на нем появляется декаль от выстрела и спецэффекты, соответствующие материалу
4. Если объект процедурно разрушаемый, то регистрируется точка попадания
5. Создается 2Д модель объекта, она делится на полигоны относительно точки попадания
5. Создается узор разрушения (несколько полигонов)
6. Полигоны отделяются по алгоритму Уайлера—Атертона
7. Модель триангулируется и переводится в 3Д модель
8. Модель рендерится вместо исходной

### [ Сценарий 8 - ИИ союзников и противников ]
todo

### [ Сценарий 9 - Sound FX ]
todo
