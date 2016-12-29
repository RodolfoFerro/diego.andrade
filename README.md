# Diego Armando Andrade Aldana
Proyectos:

1. 3-Body Problem using VPython.

# 1. 3-Body Problem using VPython.
```python
from vpython import *
import math
scene.width  = 700
scene.height = 600
scene.title  = '3-Body Problem'
scene.autoscale = False
scene.fullscreen = False
```


    <IPython.core.display.Javascript object>



    <IPython.core.display.Javascript object>



    <IPython.core.display.Javascript object>



    <IPython.core.display.Javascript object>



    <IPython.core.display.Javascript object>



    <IPython.core.display.Javascript object>



<div id="glowscript" class="glowscript"></div>



    <IPython.core.display.Javascript object>



```python
# PARAMETERS

# Masses
m1 = 3
m2 = 3
m3 = 3

e1 = 0.1 #Escale factor
e2 = 0.3 #Escale factor
e3 = 0.1 #Escale factor

# The radius as a funtion of mass (volume)
r1 = pow(m1, 1/3)*e1
r2 = pow(m2, 1/3)*e2
r3 = pow(m3, 1/3)*e3
G  = 3
dt = 0.01

# Initial positions
pos1 = vector(-2, 0, 0) #red ball
pos2 = vector(0, 0, 0) #green ball
pos3 = vector(2, 0, 0) #blue ball

# Velocitats inicials
v1 = vector(0, 0, 1.5) #red
v2 = vector(0, 1.5, 0) #green
v3 = vector(0, 0, -1.5) #blue
```


```python
# DRAWING
P1 = sphere(pos = pos1, radius = r1, color = color.red, texture=textures.stucco, shininess = 0)
P2 = sphere(pos = pos2, radius = r2, color = color.white, texture=textures.earth, shininess = 0)
P3 = sphere(pos = pos3, radius = r3, color = color.orange, texture=textures.stucco, shininess = 0)
P1.trail = curve(color = P1.color, shininess = 0)
P2.trail = curve(color = P2.color, shininess = 0)
P3.trail = curve(color = P3.color, shininess = 0)
```


```python
# MOVEMENT
# Defining an acceleration function:
def grav(p, p_m, m):
    r = p - p_m
    r_mag = mag(r)
    r_norm = norm(r)
    a = (-G*m / (r_mag**2)) * r_norm
    return a
```


```python
# Computing
while True:
    rate(60)
    # P1
    a1  = grav(P1.pos, P2.pos, m2) + grav(P1.pos, P3.pos, m3)
    dv1 = a1*dt
    v1  = v1 + dv1
    dp1 = v1*dt

    # P2
    a2  = grav(P2.pos, P1.pos, m1) + grav(P2.pos, P3.pos, m3)
    dv2 = a2*dt
    v2  = v2 + dv2
    dp2 = v2*dt

    # P3
    a3  = grav(P3.pos, P2.pos, m2) + grav(P3.pos, P1.pos, m1)
    dv3 = a3*dt
    v3  = v3 + dv3
    dp3 = v3*dt

    # Updating positions
    P1.pos = P1.pos + dp1
    P1.trail.append(pos=P1.pos)
    P2.pos = P2.pos + dp2
    P2.trail.append(pos=P2.pos)
    P3.pos = P3.pos + dp3
    P3.trail.append(pos=P3.pos)
    scene.center = P2.pos

    # Collision condition
    if mag(P1.pos-P2.pos)<(r1+r2) or mag(P1.pos-P3.pos)<(r1+r3) or (mag(P3.pos-P2.pos)<(r3+r2)):
        print("Collision !?")
        break

```


```python

```
