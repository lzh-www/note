### 1.MongoDB数据库

#### 1.1数据库概念

数据库即存储数据的仓库，可以将数据进行有序的分门别类的存储。他是独立于语言之外的软件，可以通过API去操作它。

<img src="E:\Typora笔记\images\image-20220828103205551.png" alt="image-20220828103205551" style="zoom: 80%;" />

#### 1.2MongoDB可视化软件MongoDB Compass

![image-20220828104447789](E:\Typora笔记\images\image-20220828104447789.png)

#### 1.3数据库相关概念

在一个数据库软件中可以包含多个数据仓库，在每个数据仓库中可以包含多个数据集合，每个数据集合中可以包含多条文档（具体的数据）

| 术语       | 解释说明                                                 |
| ---------- | -------------------------------------------------------- |
| database   | 数据库，mongoDB数据库软件中可以建立多个数据库            |
| collection | 集合，一组数据的集合，可以理解为Javascript中的数组       |
| document   | 文档，一条具体的数据，可以理解为Javascript中的对象       |
| field      | 字段，文档中的属性名称，可以理解为Javascript中的对象属性 |


### 2.第三模块mongoose
#### 2.1Mongoose第三方包

- 使用Node.js操作MongoDB数据库需要依赖Node.js第三方包mongoose
- 使用**npm install mongoose**命令下载
#### 2.2数据库连接

使用mongoose提供的connect方法即可连接数据库。

```js
const mongoose = require('mongoose')
mongoose.connct('mongodb://localhost/playground')
		.then(() => console.log('数据库连接成功'))
		.catch(err => console.log('数据库连接失败',err))
```

### 3.创造集合

创建集合分为二步，一是对**集合设定规则**，二是**创建集合**，创建mongoose.Schema构造函数的实例即可创建集合。

```js
//设定集合规则
const courseSchema = new mongoose.Schema({
    name: String,
    author: String,
    isPublished: Boolean
})
//创建集合并应用规则
//1.集合名称
//2.集合规则
const Course = mongoose.model('Course', courseSchema);// courses,返回Course是一个构造函数
```

### 4.创造文档

创建文档实际上就是向集合中插入数据

分为两步：

- 创建集合实例
- 调用实例对象下的save方法将数据保存到数据中

```js
//创建集合实例
const course = new Course({
    name: 'noe.js course',
    author: 'heima',
    tags: ['node','backend'],
    isPublished: true
})
//将数据保存到数据库中
course.save()
```

```js
//第二种插入文档
Course.create({name:'javascript', author: 'thor', isPublished: false}, (err, result) => {
    console.log(err);
    console.log(result);
})

Course.create({name:'javascript123', author: 'thor1', isPublished: false})
      .then(result => console.log(result))
      .catch(err => console.log(err))  
```

### 5.把现有的数据导入Mongodb

mongoimport -d 数据库名称 -c 集合名称 --file 要导入的数据文件

### 6.查询文档

```js
//根据条件查找文档（条件为空则查找所有文档）返回一组文档（数组）
Course.find().then(result => console.log(result)) //查询所有文档
Course.find({条件}).then(result => console.log(result))
```

```js
//返回一个文档（对象）
Course.findOne({条件}).then(result => console.log(result))
```


### 7.表达式查询文档
```js
//匹配大于小于
Course.find({age: {$gt: 20, $lt: 50}}).then(result => console.log(result))
```

```js
//匹配包含
Course.find({hobbies: {$in: ['打球']}}).then(result => console.log(result))
```

```js
//选择要查询的字段
Course.find().select('name author -_id').then(result => console.log(result));//-_id表示不想查询这个字段
```

```js
//将数据按照年龄进行排序
Course.find().sort('age').then(result => console.log(result));//默认升序，-age表示降序
```

```js
//skip 跳过多少条数据 limit 限制查询数量
Course.find().skip(2).limit(2).then(result => console.log(result));//
```

### 8.删除文档

```js
//删除单个,不指定条件默认删除集合第一条文档
Course.findOneAndDelete({}).then(result => console.log(result))
```

```js
//删除多个,不指定条件默认删除集合中全部文档
Course.deleteMany({}).then(result => console.log(result))
```

### 9.更新文档(修改)

```js
//更新单个
Course.updateOne({查询条件}, {要修改的值}).then(result => console.log(result))
```

```js
//更新多个
Course.updateMany({查询条件}, {要修改的值}).then(result => console.log(result))
```

### 10.Mongoose验证文档插入

```js
const Schema = new mongoose.Schema({
    title: {
        type: String,
        required: [true, '请输入文章标题'],
        minlength: [2, '文章长度不能小于2'],
        maxlength: [5, '文章最大长度不能超过5'],
        trim: true //去除字符串二端空格
    },  
    age: {
        type: Number,
        min: [10, '数值最小不能小于10'],
        max: 20
    },
    publishDate: {
        type: Date,
        default: Date.now //默认值
    },
    category: {
        type: String,
        enum:  {
            values: ['html', 'css', 'javascript', 'node.js'],
            message: '分类名称要在一定范围内才可以'
        }
    },
    author: {
        type: String,
        //自定义验证器
        validate: {
            validator: v => {
                //返回布尔值，v要验证的值
                return v && v.length > 4
            },
            message: '传入的值不符合验证规则'//自定义错误信息
        }
    }
    
})
const post = mongoose.model('Post',Schema)
post.create({title: 'ad', age: 1, category: 'hh', author: 'fff'})
    .then(result => console.log(result))
    .catch(error => {
        // 获取错误信息对象
        const err = error.errors;
        // 循环错误信息对象
        for (var attr in err) {
            //将错误信息打印到控制台中
            console.log(err[attr]['message']);
        }
    })
```

### 11.结合关联

通常不同集合的数据之间是有关系的，列如文章信息和用户信息存储在不同集合中，但文章是某个用户发表的，要查询文章的所有信息包括发表用户，就需要用到集合关联。

```js
//用户集合规则        
const userSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true
    }
})
//文章集合规则
const postSchema = new mongoose.Schema({
    title: {
        type: String
    },
    author: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User'
    }
})
//用户集合
const User = mongoose.model('User',userSchema)
//文章集合
const Post = mongoose.model('Post',postSchema)

// User.create({name: 'itheima'}).then( result => console.log(result))
// Post.create({title: '123', author: '630b35408876fee303ed9d52'}).then( result => console.log(result))

Post.find().populate('author').then( result => console.log(result))

```

























