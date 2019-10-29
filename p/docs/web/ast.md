开源工具：  
* esprima ： 从JavaScript源代码形成AST 
* estraverse：遍历树的节点并修改 
* escodegen ： 把修改完的AST再次转化为源代码。

```
const esprima = require('esprima');//JS语法树模块
const estraverse = require('estraverse');//JS语法树遍历各节点
const escodegen = require('escodegen');//JS语法树反编译模块
const AST = esprima.parseScript(jsCode);

/**
 * 
 * @param {遍历语法树} ast 
 */
function walkIn(ast){
    estraverse.traverse(ast, {
        enter: (node) => {
            toEqual(node);
            setParseint(node); 
        }
    });
}

function setParseint(node) {
    //判断节点类型 方法名称，方法的参数的数量,数量为1就增加第二个参数
    if (node.type === 'CallExpression' && node.callee.name === 'parseInt' && node.arguments.length===1){

        node.arguments.push({//增加参数，其实就是数组操作
            "type": "Literal",
            "value": 10,
            "raw": "10"
        });
    }
}

//生成目标代码
const code = escodegen.generate(ast);
```