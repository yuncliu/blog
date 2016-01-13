title: "Use tensorflow solve equation"
date: 2016-01-13 16:53:34
tags: ML
---

## Introduce

Tensorflow is a machine learn framework opensource by Google.


## Tensorflow basic
introduct basic concepts of tensorflow
### tensor

A type to contain data, scalar vector, matrix

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

## Use tensorflow sove equation

### definition
From equation Ax = y. We need to define 3 tensors to accomdate the 3 element.
- A, a constant matrix, define it as a constant tensor

```python
A = tf.constant( [[1., 2.], [3., 4.]])

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
We known that x=y/A. But here we use iteration method to solve it. In interaton method, we get a initial x, then calculate y_ = Ax, the we calcuate the deviation as y - y_
or something. We just need to minimize the deviation, then we
will got the x. So define the deviation as
```python
y_ = tf.matmul(A, x)
deviation = tf.reduce_sum(tf.square(y - y_))
```
Here the y_ is output tensor of operation tf.matmul which take A and x as input. 

deviation is output tensor of operation tf.reduce_sum which
calculate (y - y_)^2

### iteration step
We've defined several tersors and operations. Then we need to define how do minimize the deviation. The GradientDescent method is a common used method to minimize deviations
```python
train_step = tf.train.GradientDescentOptimizer(0.01).minimize(deviation)
```

### Calculate
```python
init = tf.initialize_all_variables()
sess = tf.Session()
sess.run(init)
for i in range(10000):
    sess.run(train_step)
print(sess.run(x))

```
Then we will get what we want.
