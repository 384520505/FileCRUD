# H5+App 实现对本地文件内容的增删改查
# 在进行增删改查的过程中，始终以json对象的形式进行操作

- 该插件只能在webapp环境中使用，浏览器、node环境不支持

# 使用

## FileCRUD：
- params： {fileName, type}, 
- fileName:必填项，文件名称，需要带有文件类型后缀，eg: test.txt; 
- type:选填项，文件存储类型，默认值为plus.io.PRIVATE_DOC，其他类型请参考，H5+App io章节中type解析

## writeConToFile：
- params：text
- text：json对象数据类型，写入的文本内容，内容可以为空

## readConOfFile：
- params：measure，measure：undefined,读取json对象的中的所有内容； measure：['name'],只读取json对象中的name属性

## updataConToFile：
- params：{name:'zhangsan', age:18, sex:'nan'},将文件中的name、age、sex属性值更新，若源文件中没有sex属性，则添加sex属性

## deletedConToFile：
- params：measure，measure：undefined,删除json对象的中的所有内容； measure：['name'],只删除json对象中的name属性

### 引入插件
- <script src='js/FileCRUD.js'></script>
- 扩展 plusready API加载完毕后调用此插件的功能 
```javascript 
	document.addEventListener( "plusready", function(){
		const FileCrud = new FileCRUD({ fileName: 'setting.txt', type: plus.io.PRIVATE_DOC });
		// 获取文件操作对象
		const { writeConToFile, readConOfFile, updataConToFile, deletedConToFile } = FileCrud;
		// 写内容到 setting.txt文件中
		const text = {name:'zhangsna', age:18};
		// 以对象的形式写入文件中
		writeConToFile(text)
		.then(res => {
			console.log(JSON.stringify(res));
		})
		.catch(error => {
			console.log(error)
		});
		
		// 读取setting.txt中的内容
		// 以对象的形式读出内容，不写参数表示读取对象中的所有字段，也可以添加参数数组 ['name'] 则只读取name字段
		readConOfFile(['name'])
		.then(res=>{
			console.log(JSON.stringify(res))
		})
		.catch(error=>{
			console.log(error);
		});
		
		// 更新内容
		updataConToFile({name:'zhangsan', age:18, sex:'nan'})
		.then(res=>{
			console.log(JSON.stringify(res));
		})
		.catch(error=>{
			console.log(error);
		});
		
		// 删除内容
		deletedConToFile(['sex'])
		.then(res=>{
			console.log(JSON.stringify(res));
		})
		.catch(error=>{
			console.log(error)
		})
		console.log('deleteFile')
	});
```
具体使用，请参考index.html中的案例

