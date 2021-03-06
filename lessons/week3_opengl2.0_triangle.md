# Урок 1 - OpenGL 2.0: Первый треугольник



## План работы:

1. Для начала работы с библиотекой OpenGL необходимо установить Visual Studio и иметь базовые навыки программирования на С++
2. Для обсуждения проектов рекомендую создать аккаунт в GitHub (для новичков есть небольшая инструкция по [ссылке](https://github.com/aktumar/Learning_Computer_Graphics/blob/master/lessons/instructions/GitHub.md))
3. Для удобного просмотра данного файла с лекциями рекомендую использовать маркдаун редакторы (Typora, Notion, VisualCode)
4. А также необходимо установить дополнительные библиотеки (для новичков есть небольшая инструкция по [ссылке](https://github.com/aktumar/Learning_Computer_Graphics/blob/master/lessons/instructions/GitHub.md/Library_settings.md))  (ссылку на эти библиотеки можно найти ниже, в разделе "Библиотеки")

P.S. Для первого знакомства с компьютерной графикой будет достаточно одной библиотеки "freeglut 3.0.0 MSVC Package" (https://www.transmissionzero.co.uk/software/freeglut-devel/). Однако в следующих лекциях мы будем рассматривать с вами новые стандарты OpenGL 3.0 и GLSL. 



## 1. Теория

OpenGL (Open Graphics Library) — спецификация, определяющая платформонезависимый программный интерфейс для написания приложений, использующих двумерную и трёхмерную компьютерную графику.

Основным принципом работы OpenGL является получение наборов векторных графических примитивов в виде точек, линий и треугольников с последующей математической обработкой полученных данных и построением растровой картинки на экране и/или в памяти. 

OpenGL является низкоуровневым процедурным API, что вынуждает программиста диктовать точную последовательность шагов, чтобы построить результирующую растровую графику. С одной стороны, такой подход требует от программиста глубокого знания законов трёхмерной графики и математических моделей, с другой стороны — даёт свободу внедрения различных инноваций.

Существует ряд библиотек, созданных поверх или в дополнение к OpenGL. Например, библиотека GLU, являющаяся практически стандартным дополнением OpenGL и всегда её сопровождающая, построена поверх последней, то есть использует её функции для реализации своих возможностей. Другие библиотеки, как, например, GLUT и SDL, созданы для реализации возможностей, недоступных в OpenGL. К таким возможностям относятся создание интерфейса пользователя (окна, кнопки, меню и др.), настройка контекста рисования (область рисования, использующаяся OpenGL), обработка сообщений от устройств ввода-вывода (клавиатура, мышь и др.), а также работа с файлами.



## 2. Практика

Открываем пустой проект, создаем .cpp файл и можем приступать к выполнению следующих шагов.

```
// Включаем стандартный заголовок
#include <GL/freeglut.h>
```

> Если вы правильно выполнили 4-ый пункт в плане работы, то дальше проблем возникнуть не должно. Однако, если все таки у вас появились проблемы, то обязательно пишите на текстовом канале в Discort, постараюсь помочь.

Дальше создаем функцию `main()`. 

```
int main(int argc, char **argv){
```

В теле функции первым делом инициализируем `glut`:

```
	glutInit(&argc, argv);
```

Задаем режимы отображения для окна: GLUT_DOUBLE, к примеру, включает двойную буферизацию, буфер цвета GLUT_RGBA отвечает за цвет нашего объекта и GLUT_DEPTH за глубину (для определения переднего плана). Также задаем позицию окна на экране и размер окна (пиксель х пиксель). Теперь можно создавать OpenGL окно.

```
	glutInitDisplayMode(GLUT_DEPTH | GLUT_DOUBLE | GLUT_RGBA);
	glutInitWindowPosition(400, 100);
	glutInitWindowSize(500, 500);
	glutCreateWindow("OpenGL");
```

Попробуйте запустить этот код. Будет видно что у нас появилось окно, но оно очень быстро закроется. Поэтому нам необходимо добавить следующие функции обратного вызова: за рисование в окне отвечает команда `glutDisplayFunc()`, `glutMainLoop()`открывает определенный цикл, который ждет событие от оконной системы. 

```
	glutDisplayFunc(function);
	glutMainLoop();
}
```

Теперь попробуем начать рисование в новой функции `function`. 

	void function(void) {
	    glBegin(GL_TRIANGLES);
	    glVertex3f(0.0, 0.7, 0.0);
	    glColor3f(1, 0, 1);
	    glVertex3f(-0.7, -0.7, 0.0);
	    glColor3f(1, 1, 0);
	    glVertex3f(0.7, -0.7, 0.0);
	    glColor3f(1, 1, 1);
	    glEnd();
	
	    glutSwapBuffers();
	}

Как можно увидеть, для прорисовки одной фигуры необходимо указать начало и конец обрабатываемых точек. И даже можно задать определенный цвет каждой точке. При запуске этого кода, у вас должен получится такой треугольник:

![Image alt](https://github.com/aktumar/Learning_Computer_Graphics/blob/master/lessons/images/week3_triangle.png)


> Задание №1. Найти определение каждой команде (для себя)

> Задание №2. Какие функции обратного вызова существуют в OpenGL (для себя)

> Задание №3. Какие еще существуют примитивы, кроме GL_TRIANGLES (для себя)

> Задание №4. Попробуйте создать шахматную доску 3х3 (Выложить в GitHub, для проверки домашнего задания)

