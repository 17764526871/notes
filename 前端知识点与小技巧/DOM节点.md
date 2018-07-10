DOM (Document Object Model)



DOM ： 用来表示文档中对象的标准模型就称为DOM

节点： 页面中的所有内容都是节点

节点类型：  元素节点    Node.ELEMENT_NODE(1)

​		     属性节点     Node.ATTRIBUTE_NODE(2)

​		     文本节点     Node.TEXT_NODE(3)​

​		    注释节点    Node.COMMENT_NODE(8)

节点类型的属性： 	nodeType

​					nodeName

​					nodeValue

节点层级的属性：     		childNodes    返回所有子节点

​						children     返回所有子元素

​						parentNode   返回当前节点的父节点

​						nextElementSibling   返回下一个兄弟元素

​						previousElementSibling   返回上一个兄弟元素

节点树： 把页面中的节点以一种树状的结构组织起来,这个我们称之为节点树 又叫DOM树!!

![t_htmltre](C:\Users\18192\Desktop\ct_htmltree.gif)



通过 HTML DOM，树中的所有元素（节点）均可通过 JavaScript 进行访问    每一个节点就是一个对象  我们在操作元素时  就是把这个元素看做一个对象  然后用对象的属性和方法进行操作



操作元素的方法     

|                   |                                    |
| ----------------- | ---------------------------------- |
| appendChild()     | 把新的子节点添加到指定节点。       |
| removeChild()     | 删除子节点。                       |
| replaceChild()    | 替换子节点。                       |
| insertBefore()    | 在指定的子节点前面插入新的子节点。 |
| createAttribute() | 创建属性节点。                     |
| createElement()   | 创建元素节点。                     |
| createTextNode()  | 创建文本节点。                     |
| closeNode         | 克隆节点                           |
| setAttribute()    | 设置自定义属性的值。               |

​				

获取元素      

|                          |                                  |
| ------------------------ | -------------------------------- |
| getElementsByTagName()   | 获取带有指定标签名称的所有元素。 |
| getElementsByClassName() | 获取带有指定类名的所有元素。     |
| getElementsByName        | 获取带有指定name属性的所有元素   |
| querySelector()          | 获取满足条件的第一个元素         |
| querySelectorAll()       | 获取满足条件的所有元素。         |
| getAttribute()           | 获取自定义属性的值。             |
| getElementById()         | 获取带有指定 ID 的元素。         |

