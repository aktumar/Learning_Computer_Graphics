# (10 неделя) - OpenGL 3.0: Матрицы преобразования



## План работы: 

## 1. Теория

## 2. Практика

```
GLuint viewLoc;
glm::mat4 view(1);

viewLoc = glGetUniformLocation(program, "view");

//	view = glm::rotate(view, -45.0f, glm::vec3(0, 1, 0));
//	view = glm::translate(view, glm::vec3(1.0f, 1.0f, 1.0f));
//      view = glm::scale(view, glm::vec3(2.0f, 2.0f, 2.0f));

view = glm::rotate(view, 0.1f, glm::vec3(0, 1, 0));
glUniformMatrix4fv(viewLoc, 1, GL_FALSE, glm::value_ptr(view));

glutIdleFunc(myIdle);


void myIdle()
{
	view = glm::rotate(view, 0.1f, glm::vec3(0, 1, 0));
	glUniformMatrix4fv(viewLoc, 1, GL_FALSE, glm::value_ptr(view));
	glutPostRedisplay();
}


```

