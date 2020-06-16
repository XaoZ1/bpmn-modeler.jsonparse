# bpmn-modeler.jsonparse.js

本依赖文件是对[bpmn-js](https://github.com/bpmn-io/bpmn-js) 的源码改写.
用以达到可以读取json和模型导出为json格式的能力.

## Installation

```javascript
<script src="/bpmn-modeler.jsonparse.js"></script>
```

## Usage

与[bpmn-js](https://github.com/bpmn-io/bpmn-js)的创建方式保持一致

创建bpmn实例
```javascript

var bpmnModeler = new BpmnJS({
	container: '#canvas',
	keyboard: {
		bindTo: window
	}
});
```

| 参数 | value |
| --- | --- |
|type|'JSON'/'XML'|
|dict|Object|

importXML的第二个参数可选"XML", "JSON"
```javascript
import controlDict from './controlDict'

bpmnModeler.importXML(bpmnXML, {type: 'JSON', dict: controlDict}, function(err) {
	if (err) {
		return console.error('could not import BPMN 2.0 diagram', err);
	}
	...
	// add marker
	canvas.addMarker('SCAN_OK', 'needs-discussion');
});
```

saveXML的第二个参数可选"XML", "JSON"
```javascript
import controlDict from './controlDict'

bpmnModeler.saveXML({ format: true }, {type: 'JSON', dict: controlDict}, function(err, xml) {
	if (err) {
		return console.error('could not import BPMN 2.0 diagram', err);
	}
	...
	console.log('DIAGRAM', xml);
});
```

json示例
```javascript
{
	"id": "Definitions_1",
	"name": "",
	"process": [
		{
			"id": "Process_1",
			"name": "",
			"processType": "",
			"isExecutable": "false",
			"properties": [],
			"flowElements": {
				"startEvent": [
					{
						"id": "StartEvent_1",
						"name": "",
						"outgoing": [
							"Flow_1yzb5lg"
						]
					},
				],
				"task": [
					{
						"id": "Activity_0bpcogn",
						"name": "",
						"incoming": [
							"Flow_1yzb5lg"
						]
					},
				],
				"sequenceFlow": [
					{
						"id": "Flow_1yzb5lg",
						"sourceRef": "StartEvent_1",
						"targetRef": "Activity_0bpcogn"
					},
				]
			},
			"artifacts": {},
			"extensionElements": {}
		}
	],
	"diagrams":[
		{
			"id": "BPMNDiagram_1",
			"name": "",
			"plane": {
				"id":"BPMNPlane_1",
				"bpmnElement": "Process_1",
				"edges": [
					{
						"id":"Flow_1yzb5lg_di",
						"bpmnElement": "Flow_1yzb5lg",
						"waypoint": [
							{
								"x": "209",
								"y": "120"
							},
							{
								"x": "340",
								"y": "120"
							}
						]
					}
				],
				"shapes": [
					{
						"id":"_BPMNShape_StartEvent_2",
						"bpmnElement":"StartEvent_1",
						"bounds":{
							"width": "36.0",
							"height": "36.0",
							"x": "173.0",
							"y": "102.0"
						}
					},
					{
						"id":"Activity_0bpcogn_di",
						"bpmnElement":"Activity_0bpcogn",
						"bounds":{
							"width": "100",
							"height": "80",
							"x": "340.0",
							"y": "80.0"
						}
					},
				]
			}
		}
	]
}

```

# controlDict
**controlDict** 为jSON数据与BMPN模型对应关系的字典,属性如下:

| 参数 | 说明 |
| --- | --- |
|attrs|普通参数|
|enumerable|可枚举属性|
|nonEnumerable|不可枚举属性|

因为bpmn模型对不同属性设置了不同的组装类型，在json中统一为某字段属性, s所以在转换数据时需要对不同类型属性做单独处理，故此需要配置**controlDict**

## License
仅供学习交流使用.
同样也遵循 [bpmn.io license](http://bpmn.io/license).