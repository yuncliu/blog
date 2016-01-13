title: "Use tensorflow solve equation (iteration method)"
date: 2016-01-13 16:53:34
tags: ML
---

## Introduce

Tensorflow is a machine learn framework opensource by Google.
Tensorflow is very flexible, we use it to process interation
to solve an equation here.

## Tensorflow basic
introduct basic concepts of tensorflow. Tensorflow have these basic
elements.

### tensor

A type to contain data, scalar, vector, matrix ... n-dimension array

### operation

A node which do some compulate job. Take one or more tensors as
inputs and produce a output tensor.  Also can take no input.

### graph
A set of nodes

## Equation

Ax = y
- A, coefficient matrix

``` python
A = [1, 2]
    [3, 4]

```
- x, the unknown
- y, left side

``` python
y = [10]
    [22]

```
So it is very easy to get out x

## Use tensorflow slove equation

### definition
From equation Ax = y. We need to define 3 tensors to accomdate the 3 element.
- A, a constant matrix, define it as a constant tensor

```python
A = tf.constant([[1., 2.], [3., 4.]])

```
- x, unkown, define it as a variable tensor, initialize it as
zeros

```python
x = tf.Variable(tf.zeros([2, 1]))

```
- y, a constant matrix, define it as a constant tensor

```python
y = tf.constant([[10.], [22.]])
```
We known that x=y/A. But here we use iteration method to solve it.
In interaton method, we get a initial x, then calculate yy = Ax,
the we calcuate the deviation as y - yy or something. We just need
to minimize the deviation, then we will got the x. So define the
deviation as
```python
yy = tf.matmul(A, x)
deviation = tf.square(y - yy)
```
Here the yy is output tensor of operation tf.matmul which take A and x as input.

deviation is output tensor of operation tf.square calculates (y - yy)^2

### iteration step
We've defined several tersors and operations. Then we need to
define how do minimize the deviation. The GradientDescent
method is a common used method to minimize deviations

```python
train_step = tf.train.GradientDescentOptimizer(0.01).minimize(deviation)
```

### Calculate
Iterate 10000 times
```python
init = tf.initialize_all_variables()
sess = tf.Session()
sess.run(init)
for i in range(10000):
    sess.run(train_step)
print(sess.run(x))
```
Then result you will get.
