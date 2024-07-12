# vim

# 简单使用

1.普通模式（命令操作模式）

2.插入模式

insert i

编辑模式-》普通模式 esc

# 移动

hjkl

h 向左

l 向右

j 向下

k 向上

# 翻页

ctrl F 向下一页

ctrl B 向上一页

ctrl E

ctrl Y

shift g  （大写G）全文末尾

gg 小写 开头

number +gg  //55 gg 跳跃到55行

# 不同方式编辑以及跳跃单词

i 光标位置的前面插入

a 光标位置的后面插入

o 直接enter到下一行输入

x 删除光标所在字符

dd 删除整个一行

u 撤销

dw 移除当前所在光标往后的单词

b 跳跃单词首字母

e 跳跃单词最后

w 跳跃下一个单词的首字母

b e w 配合shift 联合操作 大跳

# 跳跃行首行尾

shift +6 ^ 跳跃到本行的开头

shift +4 $ 跳跃到本行末尾

在普通模式里，千万别使用退格键 backspace 和delete

# 大括号跳跃函数段落

{}  跳跃到左右大括号后

# vim复制剪切粘贴

p 拿到删除后的内容 释放

yw 复制一个单词

y$ 从当前开始，往后复制到行末尾 p 粘贴

# visual可视化模式

v -》 hjkl 操作

y p

V 大写v 操作行

gg v G 删除全文

v +跳跃命令

v o  移动到选中的开始 再按回到末尾

0 补全角落

vaw 快速选择单词

vab 包含括号

vaB 包含大括号

va<  包含尖括号 删除

v shift <> 缩进

v shift +` ~ 字母大小写转换

v +u 全部转换成小写

U 大写

# 查找和替换

/const  查找const    按n 跳跃至下一个const

:s/const/let/g 整行const 替换成let

:%s/const/let/g 全文const替换成let

:set number 临时显示行号

:9,15s/const/let/g    9行到15行替换

:%s/const/let/gc  带提示 全文const替换成let





# vim的基础配置