## R语言table函数
###### author: HongyuYin
###### email: hyhyin@163.com
###### Notes: 示例代码来源于 R Documentation
<br>

### 1 table()函数的基本形式

``` R
table(...,               
      # 可以传入一个或多个对象，需要可以被解释为分类变量 
      
      exclude = ,        
      # 设定需要exclude的某个因子，如果设置成NULL，那么同时表示useNA参数"always"
      
      useNA = c("no","ifany","always"),
      # 设定在table中是否包含缺失值
      
      dnn = list.names(),
      # 设定函数结果的维度的名字

      deparse.level = 1
      # 见例3
)
```

###### 例1 exclude参数

``` R
a <- rep(c(NA, 1/0:3), 10)
table(a)
table(a, exclude = NULL)
b <- factor(rep(c("A","B","C"), 10))
table(b)
table(b, exclude = "B")
d <- factor(rep(c("A","B","C"), 10), levels = c("A","B","C","D","E"))
table(d, exclude = "B")
print(table(b, d), zero.print = ".")
```

###### 例2 useNA参数

``` R
## Two-way tables with NA counts. The 3rd variant is absurd, but shows
## something that cannot be done using exclude or useNA.
with(airquality,
   table(OzHi = Ozone > 80, Month, useNA = "ifany"))
with(airquality,
   table(OzHi = Ozone > 80, Month, useNA = "always"))
with(airquality,
   table(OzHi = Ozone > 80, addNA(Month)))
```

###### 例3 deparse.level和dnn参数

``` R
a <- letters[1:3]
table(a, sample(a))                    # dnn is c("a", "")
table(a, sample(a), deparse.level = 0) # dnn is c("", "")
table(a, sample(a), deparse.level = 2) # dnn is c("a", "sample(a)")
```

### 2 table()输出对象的操作
* addmargins

``` R
a <- letters[1:3]
cttab = table(a, sample(a))
addmargins(cttab)  
```
* dimnames

``` R
a <- letters[1:3]
cttab = table(a, sample(a))
dimnames(cttab)  
```