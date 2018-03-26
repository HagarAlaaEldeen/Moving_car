# Moving_car
from OpenGL.GL import *
from OpenGL.GLU import *
from OpenGL.GLUT import *
import numpy as np
from math import *

def myInit():
    glMatrixMode(GL_PROJECTION)
    glClearColor(1, 1, 1, 1)   # clear background
    glClear(GL_COLOR_BUFFER_BIT)
    gluPerspective(60,1,0.1,50)
    gluLookAt(10, 10, 10 ,0, 0, 0, 0, 1, 0)

x=0
angle=0
y=0

#white-signs
def signs(z):
    glLoadIdentity()
    glColor3f(1, 1, 1)
    glTranslate(z-y , 0, 1)
    glScale(1.5, 0.1, 1)
    glutSolidCube(2)

def draw():
    glClear(GL_COLOR_BUFFER_BIT)
    global x
    global y
    #route
    glMatrixMode(GL_MODELVIEW)
    glLoadIdentity()
    glColor3f(0.78, 0.80, 0.78)
    glTranslate(-y, 1.25, 2)
    glScale(30, 0.5, 2.75)
    glutSolidCube(2)

    #signs
    for z in range (-50,20,8):
        signs(z)
#car
    #first cube
    glLoadIdentity()
    glColor3f(.45, .45, .85)
    glTranslate(x,0,0)
    glScale(1,0.25,0.5)
    glutSolidCube(5)

    glLoadIdentity()  #second cube
    glTranslate(x,.25*5,0)
    glScale(0.5, 0.25, 0.5)
    glutSolidCube(5)

#black torus
    global angle
    glColor3f(0, 0, 0)
    glLoadIdentity()
    glTranslate(x+2.5,-2.5*.25,2.5*0.5)
    glRotatef(angle,0,0,1)
    glutWireTorus(0.125,.5,12,8)

    glColor3f(0, 0, 0)
    glLoadIdentity()
    glTranslate(x+2.5, -2.5 * .25, -2.5 * 0.5)
    glRotatef(angle, 0, 0, 1)
    glutWireTorus(0.125, .5, 12, 8)

    #hidde-torus
    #glColor3f(0, 0, 0)
    #glLoadIdentity()
    #glTranslate(x-2.5, -2.5 * .25, -2.5 * 0.5)
    #glRotatef(angle, 0, 0, 1)
    #glutWireTorus(0.125, .5, 12, 8)

    glColor3f(0, 0, 0)
    glLoadIdentity()
    glTranslate(x-2.5, -2.5 * .25, 2.5 * 0.5)
    glRotatef(angle, 0, 0, 1)
    glutWireTorus(0.125, .5, 12, 8)


    if x <= 8:
       x+=0.005
       angle-=0.25
    else:
        x=-8


    if y<=7:
       y+=0.005
    else:
       y=0


    glFlush()

glutInit()
glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB)
glutInitWindowSize(500, 500)
glutCreateWindow(b"Moving_Car")
glutDisplayFunc(draw)
glutIdleFunc(draw)
myInit()
glutMainLoop()
