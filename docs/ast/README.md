### 测试1
```javascript
//input
console.log('123')
console.error('dddd')
//output
console.warn('123')
console.error('dddd')
```

```javascript
module.exports = function (
  fileInfo, // 当前处理文件的相关信息，包括文件路径与内容
  api, // jscodeshift 提供的接口
  options // 通过 jscodeshift CLI 传入的参数
) {
  const { source, path } = fileInfo;
  const { jscodeshift: j } = api;
  const root = j(source);  // 解析代码获得 AST

  // 在这里编写操作 AST 的代码
  const logExpression=root.find(j.Identifier,{name:'log'})
  logExpression.replaceWith((nodePath)=>{
    let  {node}=nodePath
    node.name='warn'
    return node
  })
  
  return root.toSource()

  //return root.toSource({ quote: 'single' }); // 将 AST 转换为代码字符串后返回
}
```

```javascript
module.exports = function (
  fileInfo, // 当前处理文件的相关信息，包括文件路径与内容
  api, // jscodeshift 提供的接口
  options // 通过 jscodeshift CLI 传入的参数
) {
  const { source, path } = fileInfo;
  const { jscodeshift: j } = api;
  const root = j(source);  // 解析代码获得 AST

  root.find(j.MemberExpression,{
    object:{
      name:'app'
    },
    property:{
     name:'get'
    }
  }).find(j.Identifier,{name:'get'}).forEach((path)=>{
    j(path).replaceWith(j.identifier('post'))
  }) 
   
  
  root.find(j.ExpressionStatement).at(0).insertBefore(j(`console.log('123123') \n`).find(j.ExpressionStatement).__paths[0].value)
    //.forEach((path)=>{
   //j(path).insertBefore(
    //j(`console.log('123123')`).find(j.ExpressionStatement).__paths[0].value
     //)
 // })

  return root.toSource()

  //return root.toSource({ quote: 'single' }); // 将 AST 转换为代码字符串后返回
}
```