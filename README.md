# Sispak_Assign1_Task1
#### Yoshua Lukas - 1313617021 
#### Ilmu Komputer 2017
Repositori ini dibuat untuk memenuhi tugas mata kuliah Sistem Pakar semester 112 Ilmu Komputer UNJ, tentang 2d Affine Transformation yang terdiri dari:
1. Scaling
2. Translation
3. Rotation
4. Projectives
- Code saya ada di file jupyter notebook
## Library
Library yang digunakan adalah numpy, matplotlib dan string
```python
import matplotlib.pyplot as plt
import numpy as np
import string
```
## Objek Transformasi & Matriks Identitas
Buat Persegi yang akan dijadikan objek transformasi
```python
# 4 Buah Titik dengan lokasi berbeda
a, b, c, d = (2, 2, 0), (2, -2, 1), (-2, -2, 2), (-2, 2, 3)

# bentuk matriksnya
A = np.array([a, b, c, d])

# matriks identitas
I = np.eye(3)
```
## Function Matriks Identitas
```python
# Matriks Identitas
def identity(A):
    xs = []
    ys = []
    for row in A:
        output_row = I @ row
        x, y, i = output_row
        xs.append(x)
        ys.append(y)
    xs.append(xs[0])
    ys.append(ys[0])
    return xs, ys
```
## Plotting Matriks Scale
```python
def plot_scale(A, xs, ys):
    warna1 = 'green'
    warna2 = 'red'
    fig = plt.figure()
    ax = plt.gca()
    xs_scale = []
    ys_scale = []
    for row in A:
        output_row = scale @ row
        x, y, i = row
        x_scale, y_scale, i_scale = output_row
        xs_scale.append(x_scale)
        ys_scale.append(y_scale)
        c, c_scale = warna1, warna2
        plt.scatter(x, y, color = c)
        plt.scatter(x_scale, y_scale, color=c_scale)
    xs_scale.append(xs_scale[0])
    ys_scale.append(ys_scale[0])
    plt.plot(xs, ys, color="green")
    plt.plot(xs_scale, ys_scale, color="red")
    plt.title("Scaling")
    ax.set_xticks(np.arange(-5, 5, 1))
    ax.set_yticks(np.arange(-5, 5, 1))
    return plt.grid(), plt.show()
```
Deklarasi Matriks Scale akan diperbesar 2 kali dari bentuk aslinya

```python
# matriks scaling (diperbesar 2 kali)
scale = np.array([[2, 0, 0], 
                  [0, 2, 0], 
                  [0, 0, 1]])
xs , ys = identity(A)
plot_scale(A, xs, ys)
```
![alt text](https://github.com/yoshualukash/Sispak_Assign1_Task1/blob/master/img/scaling.jpg "Scaling")

## Plotting Matriks Translation
```python
def plot_translation(A, xs, ys):
    warna1 = 'green'
    warna2 = 'red'
    fig = plt.figure()
    ax = plt.gca()
    xs_trans = []
    ys_trans = []
    for row in A:
        output_row = trans @ row
        x, y, i = row
        x_trans, y_trans, i_trans = output_row
        xs_trans.append(x_trans)
        ys_trans.append(y_trans)
        c, c_trans = warna1, warna2
        plt.scatter(x, y, color = c)
        plt.scatter(x_trans, y_trans, color=c_trans)
    xs_trans.append(xs_trans[0])
    ys_trans.append(ys_trans[0])
    plt.plot(xs, ys, color="green")
    plt.plot(xs_trans, ys_trans, color="red")
    plt.title("Translation")
    ax.set_xticks(np.arange(-5, 5, 1))
    ax.set_yticks(np.arange(-5, 5, 1))
    return plt.grid(), plt.show()
```
Deklarasi Matriks Translation = 1 kekanan, 1 keatas
```python
# matriks translation (translasi 1 kekanan, 1 keatas)
trans = np.array([[1, 0, 1],
                  [0, 1, 1],
                  [0, 0, 1]])
plot_translation(A, xs, ys)
```
![alt text](https://github.com/yoshualukash/Sispak_Assign1_Task1/blob/master/img/translation.jpg "Translation")

## Plotting Matriks Rotation
```python
def plot_rotation(A, xs, ys):
    warna1 = 'green'
    warna2 = 'red'
    fig = plt.figure()
    ax = plt.gca()
    xs_rot = []
    ys_rot = []
    for row in A:
        output_row = rot @ row
        x, y, i = row
        x_rot, y_rot, i_rot = output_row
        xs_rot.append(x_rot)
        ys_rot.append(y_rot)
        c, c_rot = warna1, warna2
        plt.scatter(x, y, color = c)
        plt.scatter(x_rot, y_rot, color=c_rot)
    xs_rot.append(xs_rot[0])
    ys_rot.append(ys_rot[0])
    plt.plot(xs, ys, color="green")
    plt.plot(xs_rot, ys_rot, color="red")
    plt.title("Rotation")
    ax.set_xticks(np.arange(-5, 5, 1))
    ax.set_yticks(np.arange(-5, 5, 1))
    return plt.grid(), plt.show()
```
Deklarasi Matriks Rotation = 90 derajat keatas
```python
# matriks rotation (rotasi 90 derajat)
theta = np.pi//2
sin = np.sin(theta)
cos = np.cos(theta)
rot = np.array([[cos, sin, 0], 
               [-sin, cos, 0],
                    [0, 0, 1]])
plot_rotation(A, xs, ys)
```
![alt text](https://github.com/yoshualukash/Sispak_Assign1_Task1/blob/master/img/Rotation.jpg "Rotation")

## Plotting Matriks Projectives
```python
def plot_projective(A, xs, ys):
    warna1 = 'green'
    warna2 = 'red'
    fig = plt.figure()
    ax = plt.gca()
    xs_proj = []
    ys_proj = []
    for row in A:
        output_w = proj @ row
        output_row = output_w / output_w[-1]
        x, y, i = row
        x_proj, y_proj, i_proj = output_row
        xs_proj.append(x_proj)
        ys_proj.append(y_proj)
        c, c_proj = warna1, warna2
        plt.scatter(x, y, color = c)
        plt.scatter(x_proj, y_proj, color=c_proj)
    xs_proj.append(xs_proj[0])
    ys_proj.append(ys_proj[0])
    plt.plot(xs, ys, color="green")
    plt.plot(xs_proj, ys_proj, color="red")
    plt.title("Projective")
    ax.set_xticks(np.arange(-5, 5, 1))
    ax.set_yticks(np.arange(-5, 5, 1))
    return plt.grid(), plt.show()
```
Deklarasi Matriks Projectives dengan v1 = 0.1 dan v2=0.1
```python
proj = np.array([[1, 0, 1], 
                 [1, 1, 1], 
                 [0.1, 0.1, 1]])
plot_projective(A, xs, ys)
```
![alt text](https://github.com/yoshualukash/Sispak_Assign1_Task1/blob/master/img/Projective.jpg "Projectives")
