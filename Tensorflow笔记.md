# Tensorflow笔记

## 创建Tensor对象

1. 使用直接创建

   `tf.constant(张量内容，dtype=数据类型（可选）)`

2. 创建全值的

   1. 创建全零`tf.zeros(纬度)`
   2. 创建全一`tf.ones(纬度)`
   3. 创建全为指定数值`tf.fill(纬度，指定值)`

3. 创建特殊分布的

   1. 生成正态分布的`tf.random.normal(纬度， mean=均值， stddev=标准差)`
   2. 生成截断式正态分布的随机数`tf.random.truncated_normal(纬度，mean=均值， stddev=标准差)`
      1. 保证生成的随机数在，正负两倍标准差之内
   3. 生成均匀分布的随机数`tf.random.uniform(纬度，minval=最小值，maxval=最大值)`



## 常用函数

1. 理解`axis`表示操作纬度，`0：行`，`1:纵`

![image-20201215211745518](E:\book\笔记\机器学习\Tensorflow笔记.assets\image-20201215211745518.png)

 2. 计算平均值`tf.reduce_mean(张量名，axis=操作轴)`

 3. 计算张量沿着指定纬度的和`tf.reduce_sum(张量名，axis=操作轴)`

 4. `tf.Variable()`将变量标记为可训练，被标记的变量会在反向传播中记录梯度信息，在神经网络训练中，常用该函数标记待训练参数。

 5. 特性与标签的对应

    ```python
    tf.data.Dataset.from_tensor_slices((特征，标签))
    ```

	6. 使用`tf.GradientTape`进行求导计算

    ```python
    with tf.GradientTape() as tape:
        若干计算过程
    grad = tape.gradient(函数，对谁求导)
    ```

	7. 使用`tf.one_hot`可以生成独热码，即1表示是，0表非，生成数据中每行只包含一个1

    ```python
    tf.one_hot(待转换数据，depth=几类)
    # 示例
    classes = 3
    labels = tf.constant([1,0,2])
    output = tf.one_hot(labels, depth=classes)
    ```

 6. `tf.nn.softmax()`可以将输出值计算概率分布

 7. 对参数进行自减操作`assign_sub(自减内容)`

     1. 注意：自减的变量一定是一个可训练类型，即使用 `tf.Variable()`定义的

 8. `tf.argmax`返回张量沿指定纬度最大值的索引号