# H5+App 实现对本地文件的增删改查
# 在进行增删改查的过程中，始终以json数个进行操作

- 改插件只能在webapp环境中使用，浏览器、node环境不支持

# 使用
- 下载插件
- <script src='js/FileCRUD.js'></script>

- 扩展API加载完毕后调用此插件的功能 
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