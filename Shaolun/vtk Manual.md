vtk Manual
===
\# 常用对象方法
```js
// actor
newInstance()
actor.setMapper(mapper)
actor.getProperty().setEdgeVisibility(true);
actor.getProperty().setEdgeColor(0, 1, 0);
actor.getProperty().setRepresentationToSurface();

//mapper
newInstance()
mapper.setInputConnection(arrowSource.getOutputPort());

//renderer
renderer.addActor(actor)
renderer.resetCamera()
renderer.resetCameraClippingRange();

//renderWindow
renderWindow.render()

//fullScreenRenderWindow
fullScreenRenderWindow.getRenderer()
fullScreenRenderWindow.getRenderWindow()
```
## vtk basic sources
官网文档中包含了11中基本的model，分别是：
* arrowSource
* ConcentricCylinderSource
* cone
* coneSource
* cubesource
* cylindersour
* celinesource
* linesource
* planesource
* pointsource
* SLICsource
* spheresource
除此之外，vtk也允许create class，自定义的constructor，class方法和默认参数。

### 基本的vtk实例
```js
import React, { Component } from 'react'

import vtkMapper from 'vtk.js/Sources/Rendering/Core/Mapper'
import ConeSource from 'vtk.js/Sources/Filters/Sources/ConeSource'
import vtkActor from 'vtk.js/Sources/Rendering/Core/Actor'
import vtkFullScreenRenderWindow from 'vtk.js/Sources/Rendering/Misc/FullScreenRenderWindow';

class DOM extends Component{

  componentDidMount(){
    const cone = ConeSource.newInstance({ height: 2, radius: 1, resolution: 8, capping: false, direction: [0,1,0]})
    const mapper = vtkMapper.newInstance()
    const actor = vtkActor.newInstance()

    mapper.setInputConnection(cone.getOutputPort())
    actor.setMapper(mapper)

    const fullRenderer = vtkFullScreenRenderWindow.newInstance()
    const renderer = fullRenderer.getRenderer()
    renderer.addActor(actor)
    renderer.resetCamera()

    const rendererWindow = fullRenderer.getRenderWindow()
    rendererWindow.render()

    global.cone = cone
    global.ConeSource = ConeSource
  }

  render(){
    return null
  }
}

export default DOM
```
*#fullScreen模式*
这是一个创建在react组件化之上的coneSource实例，as a result，一个最基本的vtk视图从创建到渲染成功，分成下面几步：
* 通过`const cone = vtkConeSource.newInstance()`创建coneSource实例
* 通过`const mapper = vtkMapper.newInstance()`和`const actor = vtkActor.newInstance()`实例化mapper和actor
* 实例化一个`fullScreenRenderer`
* 通过fullScreenRenderer的两个方法，返回两个对象`renderer`和`renderWindow`
* 创建simple source pipeline
  * `mapper.setInputConnection(cone.getOutputPort())`
  * `actor.setMapper(mapper)`
  * `renderer.addActor(actor)`
  * `renderer.resetCamera()`
* 调用`renderWindow.render()`方法，启动webgl渲染器，开始渲染

## 通过chrome的console查看对象的属性和方法
```js
//console controls
      global.mapper = mapper;
      global.actor = actor;
      global.renderer = renderer;
      global.renderWindow = renderWindow;
      global.filter = filter
```
向全局注入变量，以便在console中查看方法名

## Calculator module

体现Calculator的实例，官方给出的example比较晦涩，建议用如下的例子来理解Calculator
```js
const fullScreenRenderer = vtkFullScreenRenderWindow.newInstance();
      const renderer = fullScreenRenderer.getRenderer();
      const renderWindow = fullScreenRenderer.getRenderWindow();


      const coneSource = vtkConeSource.newInstance({ height: 1.0 });
      const filter = vtkCalculator.newInstance();

      filter.setInputConnection(coneSource.getOutputPort());
      filter.setFormula({
        getArrays: inputDataSets => ({
          input: [],
          output: [
            { location: FieldDataTypes.CELL, name: 'Random', dataType: 'Float32Array', attribute: AttributeTypes.SCALARS },
          ],
        }),
        evaluate: (arraysIn, arraysOut) => {
          const [scalars] = arraysOut.map(d => d.getData());
          for (let i = 0; i < scalars.length; i++) {
            scalars[i] = Math.random();
          }
        },
      });

      const mapper = vtkMapper.newInstance();
      mapper.setInputConnection(filter.getOutputPort());

      // ----------------------------------------------------------------------------
      // Console Zone
    //   console.log('filter', filter);
      // ----------------------------------------------------------------------------

      const actor = vtkActor.newInstance();
      actor.setMapper(mapper);

      renderer.addActor(actor);
      renderer.resetCamera();
      // renderWindow.setContainer(querySelector('.container'))
      renderWindow.render();

      
      //console controls
      global.mapper = mapper;
      global.actor = actor;
      global.renderer = renderer;
      global.renderWindow = renderWindow;
      global.filter = filter

      // -----------------------------------------------------------
      // UI control handling
      // -----------------------------------------------------------

      fullScreenRenderer.addController(controlPanel);
      const representationSelector = document.querySelector('.representations');
      const resolutionChange = document.querySelector('.resolution');

      representationSelector.addEventListener('change', (e) => {
        const newRepValue = Number(e.target.value);
        actor.getProperty().setRepresentation(newRepValue);
        renderWindow.render();
      });

      resolutionChange.addEventListener('input', (e) => {
        const resolution = Number(e.target.value);
        coneSource.setResolution(resolution);
        renderWindow.render();

        const {dispatch} = this.props
        dispatch({
          type: 'submit',
          value: resolution
        })
        console.log(this.props.value);
      });
```
说白了，Calculator就是一个可以改变原class的对象，通过对原对象的定制可以返回一个新的对象，常用的方法有`setFormula`,`getFormula`和`setFormulaSimple`

calculator.getFormula().getArrays()在调用setFormula()之前是一个包含两个数组的对象(input和output)，其中output是一个空数组[].在调用set之后，output就变成了一个类似`{location: 3, name: "Random", dataType: "Float32Array", attribute: 0}`的数组。

而calculator在set后，就会return一个新的对象来替换之前的对象object，在后续操作中，只用output的calculator来操作即可，比如用`calculator.getOutputPort`来注入mapper。



## vtk中实例化的对象
vtk中,实例化的对象都是非常规的对象，没有包含的value，每一个key的type都是一个函数。这就要引出下面所讲的API文档中每一个方法的set/get

## set/get
这是一个缩写，意思是将某个属性的读写 。可以理解为write/read。
在vtk原文档中，由于上面所说的所有实例化的对象都没有属性值，全是方法。所以在方法中，以set开头的都是以写入新的属性值为主，return值为false或true。
以get开头的方法都是返回一个value，即可被变量获取到

## 为什么vtk中的对象的方法都有很多共有的方法？
在vtk的class的creation中，存在一个macro的class， 该类是所有actor等子类的基类，在macro.js文件中，定义了很多对macro类的操作的方法，比如`getOutputData`,`getOutputPort`等，其派生出的子类都拥有这些方法。

关于实例化对象的类型
---
一般实例化一个source，返回的对象的类型是object，但是是object下的vtkConeSource
而通过`coneSource.getOutputPort()()`返回的对象是object下定义的vtkPolyData。
查看一个变量的类型用`Object.getClassName()`来获取
验证一个变量的类型用`Obejct.isA()`来验证

`vtkConeSource`中的方法是官网构造函数中的参数
`vtkPolyData`中的方法是 set/get一些几何变量，比如：vertices,lines,polys

Calculator中evaluate的参数
---
在调用Calculator时，第二个参数有一些变量的约定，比如：`FieldDataTypes`,`AttributeTypes`,在源代码中是这样描述的：
```js
//node_modules\_vtk.js@13.5.0@vtk.js\Sources\Filters\General\Calculator\index.js
import { FieldDataTypes } from 'vtk.js/Sources/Common/DataModel/DataSet/Constants';
import { AttributeTypes } from 'vtk.js/Sources/Common/DataModel/DataSetAttributes/Constants';

```

```js
//vtk.js/Sources/Common/DataModel/DataSetAttributes/Constants
export const AttributeTypes = {
  SCALARS: 0,
  VECTORS: 1,
  NORMALS: 2,
  TCOORDS: 3,
  TENSORS: 4,
  GLOBALIDS: 5,
  PEDIGREEIDS: 6,
  EDGEFLAG: 7,
  NUM_ATTRIBUTES: 8,
};

export const AttributeLimitTypes = {
  MAX: 0,
  EXACT: 1,
  NOLIMIT: 2,
};

export const CellGhostTypes = {
  DUPLICATECELL: 1, // the cell is present on multiple processors
  HIGHCONNECTIVITYCELL: 2, // the cell has more neighbors than in a regular mesh
  LOWCONNECTIVITYCELL: 4, // the cell has less neighbors than in a regular mesh
  REFINEDCELL: 8, // other cells are present that refines it.
  EXTERIORCELL: 16, // the cell is on the exterior of the data set
  HIDDENCELL: 32, // the cell is needed to maintain connectivity, but the data values should be ignored.
};

export const PointGhostTypes = {
  DUPLICATEPOINT: 1, // the cell is present on multiple processors
  HIDDENPOINT: 2, // the point is needed to maintain connectivity, but the data values should be ignored.
};

export default {
  AttributeCopyOperations,
  AttributeLimitTypes,
  AttributeTypes,
  CellGhostTypes,
  DesiredOutputPrecision,
  PointGhostTypes,
  ghostArrayName,
};

```

在引入 `Calculator` 时引用，即可在组件中直接调用其属性值。

cutter
---
`Cutter`是一个展示一个plane在一个物体中的截面的切割对象。
使用时，需要在cutter中注入两个实例化的对象，来计算重合部分：
`cutter.setCutFunction(plane);`
`cutter.setInputConnection(cube.getOutputPort());`
plane需要的时model对象
cube需要的时data对象
结合的新对象cutter作为重合部分的model的数据源注入mapper
但这只是第一步，还需要把外部的cube也渲染进去
所以在加一层cube的pipeline
例子如下：
```js
const plane = vtkPlane.newInstance();
const cube = vtkCubeSource.newInstance();

const cutter = vtkCutter.newInstance();
cutter.setCutFunction(plane);
cutter.setInputConnection(cube.getOutputPort());

const cutMapper = vtkMapper.newInstance();
cutMapper.setInputConnection(cutter.getOutputPort());
const cutActor = vtkActor.newInstance();
cutActor.setMapper(cutMapper);
const cutProperty = cutActor.getProperty();
cutProperty.setRepresentation(vtkProperty.Representation.WIREFRAME);
cutProperty.setLighting(false);
cutProperty.setColor(0, 1, 0);
renderer.addActor(cutActor);

const cubeMapper = vtkMapper.newInstance();
cubeMapper.setInputConnection(cube.getOutputPort());
const cubeActor = vtkActor.newInstance();
cubeActor.setMapper(cubeMapper);
const cubeProperty = cubeActor.getProperty();
cubeProperty.setRepresentation(vtkProperty.Representation.WIREFRAME);
cubeProperty.setLighting(false);
renderer.addActor(cubeActor);

renderer.resetCamera();
```

imageMarchingCubes
---
作用在官方的Example中被很好的诠释，即计算一个volume的等值线值iso contour和contour轮廓值。并且通过ComputeNormals和mergePoints来处理边缘地带使得渲染结果更加细腻。可以通过Examples来观察其和原来的区别。

sampleFunction
---
`sampleFunction`是被用来获取volume边界和尺寸的采样函数
经常有两个方法：`sampleDimensions`和`modelBounds`分别获取volume的尺寸和边界，都具有set和get的方法。
比如一个包在cube中的Sphere，不断放大sphere的半径，重合部分的Volume不断缩小的过程。调用的过程如下：
```js
const sample = vtkSampleFunction.newInstance({
  implicitFunction: sphere,
  sampleDimensions: [50, 50, 50],
  modelBounds: [-0.5, 0.5, -0.5, 0.5, -0.5, 0.5],
});
```
调用在顶部引用vtkSampleFuntion方法，在实例化的过程中，要传入一个对象，该对象中包含有三个键值对，第一个`implicitFunction`是指定要被采样的volume对象，二三分别是指定volume的尺寸和在空间中的区域。  

但是该方法在单独使用调试的过程中没有work，如果需要用到的话，暂时需要加入上面提到的imageMarchingCubes的方法。

vtk的Shallow copy和deep copy
---
* js基本数据类型
在JavaScript中基本数据类型有String,Number,Undefined,Null,Boolean，在ES6中，又定义了一种新的基本数据类型Symbol,所以一共有6种

基本类型是按值访问的，从一个变量复制基本类型的值到另一个变量后这2个变量的值是完全独立的，即使一个变量改变了也不会影响到第二个变量

```js
var str1 = 'a';
var str2 = str1;
str2 = 'b';
console.log(str2); //'b'
console.log(str1); //'a'
```

* js引用数据类型

引用类型值是引用类型的实例，它是保存在堆内存中的一个对象，引用类型是一种数据结构，最常用的是Object,Array,Function类型，另外还有Date,RegExp,Error等，ES6同样也提供了Set,Map2种新的数据结构
JavaScript是如何复制引用类型的
JavaScript对于基本类型和引用类型的赋值是不一样的


当变量复制引用类型值的时候，同样和基本类型值一样会将变量的值复制到新变量上，不同的是对于变量的值，它是一个指针，指向存储在堆内存中的对象（JS规定放在堆内存中的对象无法直接访问，必须要访问这个对象在堆内存中的地址，然后再按照这个地址去获得这个对象中的值，所以引用类型的值是按引用访问）
```js

var obj1 = {a:1};
var ob2 = obj1;
obj2.a = 2;
console.log(obj1); //{a:2}
console.log(obj2); //{a:2}
在这里只修改了obj1中的a属性，却同时改变了ob1和obj2中的a属性
```
变量的值也就是这个指针是存储在栈上的，当变量obj1复制变量的值给变量obj2时，obj1,obj2只是一个保存在栈中的指针,指向同一个存储在堆内存中的对象，所以当通过变量obj1操作堆内存的对象时，obj2也会一起改变

* 浅拷贝
  >创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。
  * Object.assign({}, {}, {})
```js
  var target = {};
var source = {a:1};
Object.assign(target ,source);
console.log(target); //{a:1}
source.a = 2;
console.log(source); //{a:2}
console.log(target); //{a:1}
```
Object.assign是一个浅拷贝,它只是在根属性(对象的第一层级)创建了一个新的对象，但是对于属性的值是仍是对象的话依然是浅拷贝，

  * let a = [...b]
```js
var obj = {a:1,b:{c:1}}
var obj2 = {...obj};
obj.a=2;
console.log(obj); //{a:2,b:{c:1}}
console.log(obj2); //{a:1,b:{c:1}}

obj.b.c = 2;
console.log(obj); //{a:2,b:{c:2}}
console.log(obj2); //{a:1,b:{c:2}}
```

* 深拷贝
>将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象不会影响原对象

  * Json.stringify()
```js
var obj1 = {
    a:1,
    b:[1,2,3]
}
var str = JSON.stringify(obj1)
var obj2 = JSON.parse(str)
console.log(obj2); //{a:1,b:[1,2,3]}
obj1.a=2
obj1.b.push(4);
console.log(obj1); //{a:2,b:[1,2,3,4]}
console.log(obj2); //{a:1,b:[1,2,3]}
```

vtk源码解读
---

### /vtk.js

vtk.js是根目录下的js文件，主要定义并暴露了一个vtk函数，该函数内包含几个方法来检查传入的vtk对象的合法性。并且浅拷贝了一个model对象。

### /macro.js
macro.js是的重要程度在vtk的官方手册中也有提到，它是一切vtk model的父类，所有的actor和source都是继承于macro的属性和方法。
macro.js主要定义了一些console.log和macro的方法.//L175

在obj类中，作为所有子类的共有方法，主要方法如下：
* isDeleted()
* modified()
* onModified()
* getMTime()
* isA()
* getClassName()
* set()
* get()
* getReferenceByName()
* deleted()
* getState()// Add serialization support
* shallowCopy()//Add shallowCopy(otherInstance) support

在get中类中，定义了get方法//L356
在set类中，定义了set方法//L436

在vtkAlgorithm类的定义中，定义了 `setInputData()`, `setInputConnection()`, `getOutputData()`, `getOutputPort()` 四种重要的函数

* `setInputData`
```js
  function setInputData(dataset, port = 0) {
    if (model.inputData[port] !== dataset || model.inputConnection[port]) {
          model.inputData[port] = dataset;
          model.inputConnection[port] = null;
          if (publicAPI.modified) {
            publicAPI.modified();
          }
        }
  }
```
在model内部设置了一个inputData的数组，用来将data放置在对应的[port]中(默认是0)

* `getInputData`
```js
 function getInputData(port = 0) {
    if (model.inputConnection[port]) {
      model.inputData[port] = model.inputConnection[port]();
    }
    return model.inputData[port];
  }
```
不用传入任何的参数，直接return一个model.inputData

* `setInputConnection`
```js
  model.inputConnection[port] = outputPort;
```

在model内部又创建了一个inputConenction属性，默认的[port]还是0

* `getInputConnection`
```js
  return model.inputConnection[port]
```

* `addInputConnection`
```js
model.numberOfInputs++;
    setInputConnection(outputPort, model.numberOfInputs - 1);
```
该方法是在setIpt的基础上，再在inputConnection数组内增加一个port并add新的Connection

* `addInputData`
  同上

ok，以上就是对于Inputdata的一些方法。但是vtk的developer，除了data的set和get，还提供了若干种data的相关方法：

* `getOutputPort`
return的结果是调用getOutputData函数 内部返回的结果，函数是一个嵌套函数

另外，macro还设置了一些全局的方法：
* update()
* getNumberOfInputPorts()
* getNumberOfOutputPorts()
* getInputArrayToProcess()

除了algo，还有一种叫做event的类，包含多种处理事件的方法及其回调函数，下面将列举一些event class中包含的方法：

* off()
* on()
* invoke()

除此之外，还有一种全局的方法，`newInstance`
```js
export function newInstance(extend, className) {
  const constructor = (initialValues = {}) => {
    const model = {};
    const publicAPI = {};
    extend(publicAPI, model, initialValues);

    return Object.freeze(publicAPI);
  };

  // Register constructor to factory
  if (className) {
    vtk.register(className, constructor);
  }

  return constructor;
}
```

macro.js后面包含的就是关于路由proxy的一些算法，
最后在文档的末尾暴露了一些在文档中定义的算法：
```js
export default {
  algo,
  capitalize,
  chain,
  debounce,
  enumToString,
  event,
  EVENT_ABORT,
  formatBytesToProperUnit,
  formatNumbersWithThousandSeparator,
  get,
  getArray,
  getCurrentGlobalMTime,
  getStateArrayMapFunc,
  isVtkObject,
  keystore,
  newInstance,
  normalizeWheel,
  obj,
  proxy,
  proxyPropertyMapping,
  proxyPropertyState,
  safeArrays,
  set,
  setArray,
  setGet,
  setGetArray,
  setImmediate: setImmediateVTK,
  setLoggerFunction,
  throttle,
  traverseInstanceTree,
  TYPED_ARRAYS,
  uncapitalize,
  VOID,
  vtkDebugMacro,
  vtkErrorMacro,
  vtkInfoMacro,
  vtkLogMacro,
  vtkOnceErrorMacro,
  vtkWarningMacro,
};

```

### /Common/DataModel/PolyData

在该文档中，主要对verts，lines，polys和strips的处理和读取的方法进行了定义，方法中包含了记录每个cell的locations和types。关键代码如下：
```js
// verts
    let nextCellPts = 0;
    if (nVerts) {
      model.verts.getCellSizes().forEach((numCellPts, index) => {
        pLocs[index] = nextCellPts;
        pTypes[index] =
          numCellPts > 1 ? CellType.VTK_POLY_VERTEX : CellType.VTK_VERTEX;
        nextCellPts += numCellPts + 1;
      });

      pLocs = pLocs.subarray(nVerts);
      pTypes = pTypes.subarray(nVerts);
    }

    // lines
    if (nLines) {
      model.lines.getCellSizes().forEach((numCellPts, index) => {
        pLocs[index] = nextCellPts;
        pTypes[index] =
          numCellPts > 2 ? CellType.VTK_POLY_LINE : CellType.VTK_LINE;
        if (numCellPts === 1) {
          console.log(
            'Building VTK_LINE ',
            index,
            ' with only one point, but VTK_LINE needs at least two points. Check the input.'
          );
        }
        nextCellPts += numCellPts + 1;
      });

      pLocs = pLocs.subarray(nLines);
      pTypes = pTypes.subarray(nLines);
    }

    // polys
    if (nPolys) {
      model.polys.getCellSizes().forEach((numCellPts, index) => {
        pLocs[index] = nextCellPts;
        switch (numCellPts) {
          case 3:
            pTypes[index] = CellType.VTK_TRIANGLE;
            break;
          case 4:
            pTypes[index] = CellType.VTK_QUAD;
            break;
          default:
            pTypes[index] = CellType.VTK_POLYGON;
            break;
        }
        if (numCellPts < 3) {
          console.log(
            'Building VTK_TRIANGLE ',
            index,
            ' with less than three points, but VTK_TRIANGLE needs at least three points. Check the input.'
          );
        }
        nextCellPts += numCellPts + 1;
      });

      pLocs += pLocs.subarray(nPolys);
      pTypes += pTypes.subarray(nPolys);
    }

    // strips
    if (nStrips) {
      pTypes.fill(CellType.VTK_TRIANGLE_STRIP, 0, nStrips);

      model.strips.getCellSizes().forEach((numCellPts, index) => {
        pLocs[index] = nextCellPts;
        nextCellPts += numCellPts + 1;
      });
    }

```
### /Source/Common/Core/MatrixBuilder

MatrixBuilder中，引入了一个基于WebGL的矩阵&向量计算的library，引入了{ vec3, mat4, glMatrix }三个暴露项。
vec3:三个dimention的vector
mat4：4x4的矩阵

在文档中，定义了一个class：Transform，还有如下方法：
* rotateFromDirections()
* rotate()
* rotateX()
* rotateX()
* rotateY()
* rotateZ()
* translate()
* scale()
* 

### /Filters/Sources/ConeSource

分析一个具有代表性的model Source的example，描述的是一个几何锥体的source。

ConSource.js中，整个class中只包含了一个方法：`requestData()`
```js
  let dataset = outData[0];

  const angle = (2 * Math.PI) / model.resolution;
  const xbot = -model.height / 2.0;
  const numberOfPoints = model.resolution + 1;
  const cellArraySize = 4 * model.resolution + 1 + model.resolution;

  // Points
  let pointIdx = 0;
  const points = new window[model.pointType](numberOfPoints * 3);

  // Cells
  let cellLocation = 0;
  const polys = new Uint32Array(cellArraySize);

  // Add summit point
  points[0] = model.height / 2.0;
  points[1] = 0.0;
  points[2] = 0.0;

  // Create bottom cell
  if (model.capping) {
    polys[cellLocation++] = model.resolution;
  }

  // Add all points
  for (let i = 0; i < model.resolution; i++) {
    pointIdx++;
    points[pointIdx * 3 + 0] = xbot;
    points[pointIdx * 3 + 1] = model.radius * Math.cos(i * angle);
    points[pointIdx * 3 + 2] = model.radius * Math.sin(i * angle);

    // Add points to bottom cell in reverse order
    if (model.capping) {
      polys[model.resolution - cellLocation++ + 1] = pointIdx;
    }
  }

  // Add all triangle cells
  for (let i = 0; i < model.resolution; i++) {
    polys[cellLocation++] = 3;
    polys[cellLocation++] = 0;
    polys[cellLocation++] = i + 1;
    polys[cellLocation++] = i + 2 > model.resolution ? 1 : i + 2;
  }

  // Apply tranformation to the points coordinates
  vtkMatrixBuilder
    .buildFromRadian()
    .translate(...model.center)
    .rotateFromDirections([1, 0, 0], model.direction)
    .apply(points);

  dataset = vtkPolyData.newInstance();
  dataset.getPoints().setData(points, 3);
  dataset.getPolys().setData(polys, 1);

  // Update output
  outData[0] = dataset;
```

下面，我们从vtk实例中看开发者是怎么设置vtkSource对象的API的：
以vtkConeSource为例，在chrome中打印出来coneSource对象所有的方法，结果如下：
```js
isDeleted: ƒ ()
modified: ƒ (otherMTime)
onModified: ƒ (callback)
getMTime: ƒ ()
isA: ƒ (className)
getClassName: ƒ ()
set: ƒ ()
get: ƒ ()
getReferenceByName: ƒ (val)
delete: ƒ ()
getState: ƒ ()
shallowCopy: ƒ (other)
getHeight: ƒ ()
getRadius: ƒ ()
getResolution: ƒ ()
getCapping: ƒ ()
setHeight: ƒ setter(value)
setRadius: ƒ setter(value)
setResolution: ƒ setter(value)
setCapping: ƒ setter(value)
getCenter: ƒ ()
getCenterByReference: ƒ ()
getDirection: ƒ ()
getDirectionByReference: ƒ ()
setCenter: ƒ ()
setCenterFrom: ƒ (otherArray)
setDirection: ƒ ()
setDirectionFrom: ƒ (otherArray)
shouldUpdate: ƒ ()
getOutputData: ƒ getOutputData()
getOutputPort: ƒ getOutputPort()
update: ƒ ()
getNumberOfInputPorts: ƒ ()
getNumberOfOutputPorts: ƒ ()
getInputArrayToProcess: ƒ (inputPort)
setInputArrayToProcess: ƒ (inputPort, arrayName, fieldAssociation)
requestData: ƒ requestData(inData, outData)
__proto__: Object
```

下面来逐一分析，前若干个方法来自于macro.js中被导出的函数algo的方法：
```js
isDeleted: ƒ ()
modified: ƒ (otherMTime)
onModified: ƒ (callback)
getMTime: ƒ ()
isA: ƒ (className)
getClassName: ƒ ()
set: ƒ ()
get: ƒ ()
getReferenceByName: ƒ (val)
delete: ƒ ()
getState: ƒ ()
shallowCopy: ƒ (other)
```
这些是macro的全局方法，所有继承macro的source和model都会含有这些对象。

接下来的十余个方法：
```js
getHeight: ƒ ()
getRadius: ƒ ()
getResolution: ƒ ()
getCapping: ƒ ()
setHeight: ƒ setter(value)
setRadius: ƒ setter(value)
setResolution: ƒ setter(value)
setCapping: ƒ setter(value)
getCenter: ƒ ()
getCenterByReference: ƒ ()
getDirection: ƒ ()
getDirectionByReference: ƒ ()
setCenter: ƒ ()
setCenterFrom: ƒ (otherArray)
setDirection: ƒ ()
setDirectionFrom: ƒ (otherArray)
```
他们在coneSource中是被这样设置API的：
```js
macro.setGet(publicAPI, model, ['height', 'radius', 'resolution', 'capping']);
```
在macro.js中，定义了setGet方法：
```js
export function set(publicAPI, model, fields) {
  fields.forEach((field) => {
    if (typeof field === 'object') {
      publicAPI[`set${capitalize(field.name)}`] = findSetter(field)(
        publicAPI,
        model
      );
    } else {
      publicAPI[`set${capitalize(field)}`] = findSetter(field)(
        publicAPI,
        model
      );
    }
  });
}

// ----------------------------------------------------------------------------
// set/get XXX: add both setters and getters
// ----------------------------------------------------------------------------

export function setGet(publicAPI, model, fieldNames) {
  get(publicAPI, model, fieldNames);
  set(publicAPI, model, fieldNames);
}
```
在coneSource.js中调用setGet方法时传入了后面的属性名：`['height', 'radius', 'resolution', 'capping']`,这些时用来匹配setGet方法的参数，并且生成SetXXX和getXXX API的方法。

直到最后一个方法：`requestData` 才是真正的coneSource中定义的获取数据的方法：
```js
  function requestData(inData, outData) {
    if (model.deleted) {
      return;
    }

    let dataset = outData[0];

    const angle = (2 * Math.PI) / model.resolution;
    const xbot = -model.height / 2.0;
    const numberOfPoints = model.resolution + 1;
    const cellArraySize = 4 * model.resolution + 1 + model.resolution;

    // Points
    let pointIdx = 0;
    const points = new window[model.pointType](numberOfPoints * 3);

    // Cells
    let cellLocation = 0;
    const polys = new Uint32Array(cellArraySize);

    // Add summit point
    points[0] = model.height / 2.0;
    points[1] = 0.0;
    points[2] = 0.0;

    // Create bottom cell
    if (model.capping) {
      polys[cellLocation++] = model.resolution;
    }

    // Add all points
    for (let i = 0; i < model.resolution; i++) {
      pointIdx++;
      points[pointIdx * 3 + 0] = xbot;
      points[pointIdx * 3 + 1] = model.radius * Math.cos(i * angle);
      points[pointIdx * 3 + 2] = model.radius * Math.sin(i * angle);

      // Add points to bottom cell in reverse order
      if (model.capping) {
        polys[model.resolution - cellLocation++ + 1] = pointIdx;
      }
    }

    // Add all triangle cells
    for (let i = 0; i < model.resolution; i++) {
      polys[cellLocation++] = 3;
      polys[cellLocation++] = 0;
      polys[cellLocation++] = i + 1;
      polys[cellLocation++] = i + 2 > model.resolution ? 1 : i + 2;
    }

    // Apply tranformation to the points coordinates
    vtkMatrixBuilder
      .buildFromRadian()
      .translate(...model.center)
      .rotateFromDirections([1, 0, 0], model.direction)
      .apply(points);

    dataset = vtkPolyData.newInstance();
    dataset.getPoints().setData(points, 3);
    dataset.getPolys().setData(polys, 1);

    // Update output
    outData[0] = dataset;
  }
```

## actor.getProperty()包含的方法

```js
Lighting: ƒ ter(value)
Interpolation: ƒ ter(value)
Ambient: ƒ ter(value)
Diffuse: ƒ ter(value)
Specular: ƒ ter(value)
SpecularPower: ƒ ter(value)
Opacity: ƒ ter(value)
EdgeVisibility: ƒ ter(value)
LineWidth: ƒ ter(value)
PointSize: ƒ ter(value)
BackfaceCulling: ƒ ter(value)
FrontfaceCulling: ƒ ter(value)
Representation: ƒ ter(value)
AmbientColor: ƒ ()
AmbientColorFrom: ƒ (otherArray)
SpecularColor: ƒ ()
SpecularColorFrom: ƒ (otherArray)
DiffuseColor: ƒ ()
DiffuseColorFrom: ƒ (otherArray)
EdgeColor: ƒ ()
EdgeColorFrom: ƒ (otherArray)
Color: ƒ (r, g, b)addShaderVariable: ƒ ()
InterpolationToFlat: ƒ ()
InterpolationToGouraud: ƒ ()
InterpolationToPhong: ƒ ()
RepresentationToWireframe: ƒ ()
RepresentationToSurface: ƒ ()
RepresentationToPoints: ƒ ()
```
转译后：
```js
设置照明度：ƒter（值）
设置插值：ƒter（值）
设置 环境：ƒter（值）
设置 扩散度：ƒter（值）
设置 镜面反射：ƒter（值）
设置 镜面反射功率：ƒter（值）
设置 不透明度：ƒter（值）
设置 边缘可见性：ƒter（值）
设置 线宽：ƒter（值）
设置 点大小：ƒter（值）
设置 背面剔除：ƒter（值）
设置 前端剔除：ƒter（值）
设置 表示形式：ƒter（值）
设置 环境颜色：ƒ（）
设置 环境颜色自：ƒ（otherArray）
设置 镜面颜色：ƒ（）
设置 镜面反射颜色自：ƒ（otherArray）
设置 漫反射颜色：ƒ（）
设置 漫反射颜色自：ƒ（otherArray）
设置 边缘颜色：ƒ（）
设置 边缘颜色来自：ƒ（otherArray）
设置 颜色：ƒ（r，g，b）addShaderVariable：ƒ（）
设置 插值到单位：ƒ（）
设置 插值到Gouraud：ƒ（）
设置 插值至Phong：ƒ（）
设置 表示到线框：ƒ（）
设置 表面表示：ƒ（）
设置 表示点：ƒ（）
```

## 通过js内部函数实现vtkModel的动画机制
```js
 function animate(){

      requestAnimationFrame(animate)

      render()

    }

    function render(){
      actor.rotateY(3)

      rendererWindow.render()
    }

    animate()
```

定义一个自调用函数animate，在内部重复invoke animate()本身，即可实现动画的效果。
在render()函数中，设置每一帧的变化系数，在调用rendererWindow.render()重新渲染。

## 通过sourceCode来理解Calculator的机制
以Example1为例：
```js
 const coneSource = vtkConeSource.newInstance({ height: 1.0,resolution: 8 });
      const filter = vtkCalculator.newInstance();

      console.log('filter', filter.getFormula().getArrays());


      filter.setInputConnection(coneSource.getOutputPort());
      filter.setFormula({
        getArrays: inputDataSets => ({
          input: [],
          output: [
            { location: FieldDataTypes.CELL, name: 'Random', dataType: 'Float32Array', attribute: AttributeTypes.SCALARS },
          ],
        }),
        evaluate: (arraysIn, arraysOut) => {
          //getData()
          //filter.getOutputData().getCellData().getScalars().getData()
          console.log(arraysOut[0].getData());
            
          //const [scalars] 最后返回的scalars是一个Float32Array对象
          //const scalars 返回的是一个以上述元素为元素的一个数组
          //
          //下面的一行code等价于const [a] = [filter.getOutputData().getCellData().getScalars()].map(d=>d.getData())
          //即arrayOut等价于[filter.getOutputData().getCellData().getScalars()]
          //可能是只有一个model的关系，如果是多个model的话可能会返回多个
          const [scalars] = arraysOut.map(d => d.getData());
          for (let i = 0; i < scalars.length; i++) {
            scalars[i] = Math.random();
          }
          console.log(arraysOut[0].getData());
        },
      });

      const mapper = vtkMapper.newInstance();
      mapper.setInputConnection(filter.getOutputPort());

      // ----------------------------------------------------------------------------
      // Console Zone
      // console.log('cone :', filter);
      // console.log('cone', filter.getOutputPort()() );
      // ----------------------------------------------------------------------------

      const actor = vtkActor.newInstance();
      actor.setMapper(mapper);

      renderer.addActor(actor);
      renderer.resetCamera();
      // renderWindow.setContainer(querySelector('.container'))
      renderWindow.render();
```
根据对`coneSource`和`filter`的getOutputPort结果来看，Calculator对cell的重构起到了很关键的作用，主要是通过下面的路径来实现的：
`filter.getOutputData().getCellData().getScalars()`中有一个方法`filter.getOutputData().getCellData().getScalars().getData()`,通过对数组内的值的重新赋值，来达到对每个面的yanse的重新定义的效果。

从code最上面引用的:
```js
import { AttributeTypes } from 'vtk.js/Sources/Common/DataModel/DataSetAttributes/Constants';
import { FieldDataTypes } from 'vtk.js/Sources/Common/DataModel/DataSet/Constants';
```
来看，这些引入的对象所包含的键值对 与 `filter.getOutputData().getCellData()`所包含的属性值几乎是一样的，意味着通过对本例的模仿，可以任意修改对象中的属性，来实现不同的效果。

## 目前与源代码契合度最高的Example-ImageStreamline

调用了macro.js中newInstance的方法，and macro.obj() & macro.algo()

### imageMarchingCube-网格生成算法
很多连续算法在最后提取等值面的时候都会采用marching cube或其改进版本，可以说是很多算法的最后一步
等值面，很简单的理解，就是一个点电荷在一个真空无干扰场中形成的一个球形区域表面，这个表面的value场强就是一个等值面。

因为六面体有8个顶点，8个顶点的状态就有2^8 = 256中分布状态，但是由于六面体是有对称性的，我们通过对称性，可以简化这些状态至15种状态 

* Marching Cube 算法流程
将原始数据经过预处理之后,读入特定的数组中或者八叉树。
从网格数据体中提取一个六面体,成为当前六面体"同时获取该六面体的所有信息,例如8个顶点的值,坐标位置等。
将当前六面体8个顶点的函数值与给定等值面值C进行比较,得到该六面体的状态表。
根据当前六面体的状态表索引,找出与等值面相交的六面体棱边,并采用线性插值的方法,计算出各个交点的位置坐标。
利用中心差分法,求出当前六面体8个顶点的法向量,在采用线性插值的方法,得到三角面片各个顶点的法向。
根据各个三角面片顶点的坐标,顶点法向量进行三角面的连接。

* 系统诠释Marching cube
在三维规则数据场中构造等值面是计算机视觉也是VTK当中的一个重要的问题，Marching Cubes方法就是解决这个问题的一个成熟的被广泛使用的方法，简称MC方法。VTK当中的vtkMarchingCubes就是对这个方法的代码实现。

下面结合唐泽圣的《三维数据场可视化》和vtk的《The Design and Implementation of an Object-OrientedToolkit for 3D Graphics and Visualization》两本书的内容介绍一下MC方法。

在MC方法中, 假定原始数据是离散的三维空间规则数据场。用于医疗诊断的断层扫描仪( CT ) 及核磁共振仪( MRI ) 等产生的图象均属于这一类型。为了在这一数据场中构造等值面, 用户应先给出所求等值面的值, 设为C0。MC 方法首先找出该等值面经过的体元的位置, 求出该体元内的等值面并计算出相关参数, 以便由常用的图形软件包或图形硬件提供的面绘制功能绘制出等值面。由于这一方法是逐个体元依次处理的, 因此被称为Marching Cubes方法。

vtk原文档中描述：
vtkMarchingCubes is a filter that takes as input a volume (e.g., 3D structured point set) and generateson output one or more isosurfaces. One or more contour values must be specifiedto generate the isosurfaces. Alternatively, you can specify a min/max scalarrange and the number of contours to generate a series of evenly spaced contourvalues.

即：vtkMarchingCubes是一个过滤器，该过滤器接受一个体数据的输入（三维规则的点集），输出一个或者多个等值面。使用它，必须给等值面赋值。或者，你可以设定的一个scalar的范围和等值面的间隔来决定这个范围内的一系列的等值面的值。

几个重要的方法是（using tcl）：

void SetValue (int i, double value) 设置第i个等值面的值为value

void SetNumberOfContours (int number) 设置等值面的个数

## implicit boolean
先看一下官方的API解释：
>vtkImplicitBoolean enables boolean combinations of implicit functions like Plane, Sphere, Cylinder, and Box. Operations include union, intersection, and difference. Multiple implicit functions can be specified (all combined with the same operation).

即：vtkImplicitBoolean enables 隐式函数（如Plane，Sphere，Cylinder和Box）的布尔组合。 操作包括并集，相交和差。 可以指定多个隐式函数（全部与同一操作组合）。

vtkjs数据格式汇总
---
Loaders included:
* ZipHttpReader
* HttpDataSetReader=>.vti
* HttpSceneLoader
* STLReader
* PolyDataReader
* ElevationReader
* JSONNucleoReader
* OBJReader
* PDBReader

sampleData：
* draco
* mha
* nrrd
* obj-mtl
* pdb
* vti
* vtkjs
* vtp

vtkjs源代码loader目录
---
IO/Core=>
* DataAccessHelper
* HttpDataSetReader
* HttpSceneLoader
* ImageStream
* ResourceLoader
* Serializer
* ZipMultiDataSetReader
* ZipMultiDataSetWriter

IO/Geometry=>
* DracoReader
* STLReader
  
IO/Legacy=>
* LegacyAsciiParser
* PolyDataReader

IO/Misc=>
* ElevationReader
* ITKImageReader
* ITKPolyDataReader
* JSONNucleoReader
* JSONReader
* MTLReader
* OBJReader
* PDBRReader
* SkyboxReader

IO/XML=>
* XMLImageDataReader
* XMLImageDataWriter
* XMLPolyDataReader
* XMLPolyDataWriter
* XMLReader
* XMLWriter



threejs Loader
---
* BasisTextureLoader
* DRACOLoader
* GLTFLoader
* MMDLoader
* MTLLoader
* OBJLoader
* OBJLoader2
* PCDLoader
* PDBLoader
* PRWMLoader
* SVGLoader
* TGALoader
...

webGL Loader
---
"webgl_loader_3ds",
"webgl_loader_3mf",
"webgl_loader_3mf_materials",
"webgl_loader_amf",
"webgl_loader_assimp",
"webgl_loader_bvh",
"webgl_loader_collada",
"webgl_loader_collada_kinematics",
"webgl_loader_collada_skinning",
"webgl_loader_draco",
"webgl_loader_fbx",
"webgl_loader_fbx_nurbs",
"webgl_loader_gcode",
"webgl_loader_gltf",
"webgl_loader_gltf_extensions",
"webgl_loader_imagebitmap",
"webgl_loader_json_claraio",
"webgl_loader_kmz",
"webgl_loader_ldraw",
"webgl_loader_lwo",
"webgl_loader_md2",
"webgl_loader_md2_control",
"webgl_loader_mmd",
"webgl_loader_mmd_pose",
"webgl_loader_mmd_audio",
"webgl_loader_nrrd",
"webgl_loader_obj",
"webgl_loader_obj_mtl",
"webgl_loader_obj2",
"webgl_loader_obj2_options",
"webgl_loader_pcd",
"webgl_loader_pdb",
"webgl_loader_ply",
"webgl_loader_prwm",
"webgl_loader_stl",
"webgl_loader_svg",
"webgl_loader_texture_basis",
"webgl_loader_texture_dds",
"webgl_loader_texture_exr",
"webgl_loader_texture_hdr",
"webgl_loader_texture_ktx",
"webgl_loader_texture_pvrtc",
"webgl_loader_texture_rgbm",
"webgl_loader_texture_tga",
"webgl_loader_ttf",
"webgl_loader_vrm",
"webgl_loader_vrml",
"webgl_loader_vtk"

vtk的扩展格式
---
vtk数据和paraview数据有很多的子格式，这里要对vtk的数据格式和特点做一个了解。所有格式的共同点是：
* 使用右手笛卡尔坐标系。
* 坐标点和像元（=点之间的区域）都在文件中定义，因此可以将数据值分配给点或像元。
* 数据值可以是任意维度（标量，向量，张量）的整数或浮点数（C变量类型：int32或float）
* ASCII浮点数写有小数点（不是逗号！）；也可以使用科学计数法（例如“ 3.14E-3”）。二进制值以“ C样式”编写
* 可以将任意数量的数据集分配给点或单元格，但是由于文件只能包含一个坐标网格，因此每个数据集必须具有每个坐标点或网格单元格的数据值。不同网格上的数据集必须写入不同的文件中。
* **对于新的XML文件类型，情况并非完全如此。在这里，每个文件可能包含“一个或多个Piece元素，每个元素描述数据集的一部分”。每个片段都有其自己的关联点和单元格的定义。**
* 通过为文件名赋予连续的数字（在名称的末尾，在扩展名之前），可以实现动画效果，例如“ file001.vtk”，“ file002.vtk”等。然后可以将这些文件作为动画播放。

### Old ("Legacy") and New (XML) Format
There are two generations of file types：
* 旧的* .vtk文件格式使用ASCII标题行分隔数据部分。 数据本身可以是ASCII或二进制.
* 基于XML的新格式（扩展名：取决于；例如* .vtp（表示多边形数据），*.vtu（表示非结构化网格））将数据部分用XML标记括起来。 数据也可以存储为ASCII或二进制，但是要获取有效的XML文件，二进制数据必须经过base64编码。 此外，可以使用zlib压缩二进制数据，因此即使压缩数据是base64编码的，文件大小也比原始二进制格式小。

### Convert of data format
如果需要其他文件格式，请使用VTK工具包进行转换。 例如 编写一个Tcl脚本。 然后，您可以一步将简单的ASCII * .vtk文件转换为功能齐全的二进制压缩XML文件。

jordain提供了一种convert的回答，还没有没证实，在这里记录一下：
```s
$ npm install -g kitware/vtk-js
$ vtkDataConverter 

  Usage: vtkDataConverter [options]

  Options:

    -h, --help                output usage information
    -V, --version             output the version number
    -i, --input [file.vtk]    Input data file to convert
    -o, --output [directory]  Destination directory

    -m, --merge               Merge dataset
    -e, --extract-surface     Extract surface

    --paraview [path]         Provide the ParaView root path to use
    --sample-data [path]      Convert sample data from ParaViewData
```

对FullScreenRenderer的源码解析
---
vtkjs推荐的默认renderer是FullScreenRenderer，
然而，如果需求是一个单页面应用的话，则需要把render注入到一个DOM元素中
但是，拥有两个问题：
1. 注入后 的model明显失真
2. DOM 类的render需要的rendering模块和interacting模块非常多，猜测fullScreen类的renderer是将这些rendering模块都封装在其中

所以，想要搞清楚两个问题，需要从源代码入手：
* 从FullScreenRenderWindow/index.js的引入模块来看：
```js
import macro from 'vtk.js/Sources/macro';
import vtkOpenGLRenderWindow from 'vtk.js/Sources/Rendering/OpenGL/RenderWindow';
import vtkRenderer from 'vtk.js/Sources/Rendering/Core/Renderer';
import vtkRenderWindow from 'vtk.js/Sources/Rendering/Core/RenderWindow';
import vtkRenderWindowInteractor from 'vtk.js/Sources/Rendering/Core/RenderWindowInteractor';
import vtkInteractorStyleTrackballCamera from 'vtk.js/Sources/Interaction/Style/InteractorStyleTrackballCamera';
```
  我们的猜测是很有可能的。
在自己封装了五个renderer和controler之后，发现
渲染出来的图像是很模糊的，例如：coneSource
所以，试了试将fullScreenRenderer的源代改变了一下再封装了一个文件
引入后发现，效果还不错
命名为`FullDOMRenderer`
所以就暂时用这个吧，
但愿未来一切顺利！


与react-grid-layout的结合
---
昨晚实现了在React-grid-layout中成功的实现了vtk模块的响应式开发
但是缺点是在根组件<App/>中mount vtk模块，即vtk组件和根组件融合了，没有父子关系

原因是在vtk的div生成和渲染环节，先`document.querySelector('.react-grid-layout')`，然后再`appendChild(container)`,所以只能再App根组件层实现加载，因为如果在子组件中无法获取到 grid 的DOM
但是后期试了一下，在vtk组件的render()函数中返回了一个div#dom-div,这样便可以在本组件中获取到该div，也可以渲染到div中。

在App根组件中，是这样引入的
```js
<ResponsiveGridLayout >
    <div key="4" data-grid={{
        x: 0,
        y: 0, // puts it at the bottom
        w: 4,
        h: 3,
        i: new Date().getTime().toString(),
        type: 'bar'
        }}><DOM/></div>
</ResponsiveGridLayout>
```
如上方的代码所示，`<ResponsiveGridLayout >`的子节点，最好是div节点，因为如果是组件<DOM/>的话，不可以触发响应式的布局。
在div中设置一下grid所需要的参数。
如此一来，既实现了grid的响应式布局，又实现了App根组件的父子层级结构，岂不美哉。

react-bootstrap
---
现在需要解决渲染react grid layout的问题，怎么给模块化的组件套上一层“窗口”
于是我去查bootstrap，发现其中的modal似乎可以解决我的问题
现在先介绍一下怎么引用和使用`react-bootstrap`
1. `npm install react-bootstrap bootstrap jquery bootstrap`
2. `import 'bootstrap/dist/css/bootstrap.min.css';`//index.js
3. `import { Button } from 'react-bootstrap';`//目标组件
