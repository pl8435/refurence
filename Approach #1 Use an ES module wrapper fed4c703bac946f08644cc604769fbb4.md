# Approach #1: Use an ES module wrapper

```jsx
Write the package in CommonJS or transpile ES module 
sources into CommonJS, and create an ES module wrapper 
file that defines the named exports.
```

> CommonJS로 패키지를 작성하거나 ES 모듈 소스를 CommonJS로 변환하고 명명된 export를 정의하는 ES 모듈 래퍼 파일을 만듭니다.
> 

```jsx
Using Conditional exports, the ES module wrapper is used 
for import and the CommonJS entry point for require.
```

> 조건부 export를 사용하면 ES 모듈 래퍼가 import에 사용되고 CommonJS entry point는 require에 사용됩니다.
> 

```jsx
// ./node_modules/pkg/package.json
{
  "type": "module",
  "main": "./index.cjs",
  "exports": {
    "import": "./wrapper.mjs",
    "require": "./index.cjs"
  }
}
```

```jsx
The preceding example uses explicit extensions .mjs and 
.cjs. If your files use the .js extension, "type": "module"
will cause such files to be treated as ES modules, just 
as "type": "commonjs" would cause them to be treated as 
CommonJS. See Enabling.
```

> 앞의 예에서는 명시적 확장자 .mjs 및 .cjs를 사용합니다. 파일이 .js 확장자를 사용하는 경우 "type": "module"은 이러한 파일을 ES 모듈로 처리하게 하며, "type": "commonjs"로 인해 해당 파일이 CommonJS로 처리되는 것과 같습니다. 링크를 참조하십시오.
> 

```jsx
// ./node_modules/pkg/index.cjs
exports.name = 'value';
```

```jsx
// ./node_modules/pkg/wrapper.mjs
import cjsModule from './index.cjs';
export const name = cjsModule.name;
```

```jsx
In this example, the name from import { name } from 'pkg' 
is the same singleton as the name from 
const { name } = require('pkg').
```

> 이 예에서 import { name } from 'pkg'의 이름은 const { name } = require('pkg')의 이름과 동일한 단일 항목입니다.
> 

```jsx
Therefore === returns true when comparing the two names 
and the divergent specifier hazard is avoided.
```

> 따라서 === 는 두 이름을 비교할 때 true를 반환하고 지정자가 다를 위험을 방지합니다.
> 

```jsx
If the module is not simply a list of named exports, 
but rather contains a unique function or object export 
like module.exports = function () { ... }, or if support 
in the wrapper for the import pkg from 'pkg' pattern is 
desired, then the wrapper would instead be written to 
export the default optionally along with any named exports 
as well:
```

> 모듈이 단순히 지정된 exports 목록이 아니라 module.exports = function () { ... }와 같은 고유한 함수 또는 객체 export를 포함하거나 'pkg' 패턴에서 pkg import 에 대한 래퍼가 지원되거나 원하는 경우 래퍼는 이름이 지정된 export와 함께 선택적으로 기본값을 export하도록 대체됩니다.
> 

```
import cjsModule from './index.cjs';
export const name = cjsModule.name;
export default cjsModule;
```

```jsx
This approach is appropriate for any of the following 
use cases:
```

> 이 접근 방식은 다음 사용 사례에 적합합니다.
> 

```jsx
The package is currently written in CommonJS and the 
author would prefer not to refactor it into ES module 
syntax, but wishes to provide named exports for ES module 
consumers.
```

> 패키지는 현재 CommonJS로 작성되었으며 작성자는 이를 ES 모듈 구문으로 리팩토링하지 않고 ES 모듈 소비자를 위한 지정된 export를 제공하고자 합니다.
> 

```jsx
The package has other packages that depend on it, and the 
end user might install both this package and those other 
packages.
```

> 패키지에는 이에 의존하는 다른 패키지가 있으며 최종 사용자는 이 패키지와 다른 패키지를 모두 설치할 수 있습니다. (상속되거나 하는 패키지가 잇으면)이 접근 방식은 다음 사용 사례에 적합합니다.
> 

```jsx
For example a utilities package is used directly in an 
application, and a utilities-plus package adds a few more 
functions to utilities. Because the wrapper exports 
underlying CommonJS files, it doesn’t matter if 
utilities-plus is written in CommonJS or ES module syntax; 
it will work either way.
```

> 예를 들어 유틸리티 패키지는 응용 프로그램에서 직접 사용되며 유틸리티 플러스 패키지는 유틸리티에 몇 가지 기능을 더 추가합니다. 래퍼는 기본 CommonJS 파일을 내보내기 때문에 utility-plus가 CommonJS 또는 ES 모듈 구문으로 작성되었는지 여부는 중요하지 않습니다. 어느 쪽이든 작동합니다.
> 

```jsx
The package stores internal state, and the package author 
would prefer not to refactor the package to isolate its 
state management.
```

> 패키지는 내부 상태를 저장하고 패키지 작성자는 상태 관리를 분리하기 위해 패키지를 리팩토링하지 않는 것을 선호합니다.
> 

```jsx
See the next section.
```

> 다음 섹션을 참조하십시오.
> 

```jsx
A variant of this approach not requiring conditional 
exports for consumers could be to add an export, 
e.g. "./module", to point to an all-ES module-syntax
version of the package.
```

> 소비자에 대한 조건부 export을 요구하지 않는 이 접근 방식의 변형은 export을 추가하는 것일 수 있습니다. 예를 들어 "./module"은 패키지의 모든 ES 모듈 구문 버전을 가리킵니다.
> 

```jsx
This could be used via import 'pkg/module' by users who 
are certain that the CommonJS version will not be loaded 
anywhere in the application, such as by dependencies; 
or if the CommonJS version can be loaded but doesn’t 
affect the ES module version (for example, because the 
package is stateless):
```

> 이것은 CommonJS 버전이 종속성과 같이 애플리케이션의 어느 곳에서도 로드되지 않을 것이라고 확신하는 사용자가 'pkg/module' export를 통해 사용할 수 있습니다. 또는 CommonJS 버전을 로드할 수 있지만 ES 모듈 버전에 영향을 미치지 않는 경우(예: 패키지가 상태 비저장이기 때문에):
> 

```
// ./node_modules/pkg/package.json
{
  "type": "module",
  "main": "./index.cjs",
  "exports": {
    ".": "./index.cjs",
    "./module": "./wrapper.mjs"
  }
}
```

```
Wrapper: 자바스크립트와 같은 프로그래밍 언어에서 래퍼는 하나 이상의 다른 기능들을 호출하기 위한 기능이며, 때로는 순전히 편의상, 때로는 프로세스에서 약간 다른 작업을 하도록 적응시키는 기능이다.

모듈 패턴: 모듈이란 전제 어플리케이션의 일부를 독립된 코드로 분리하여 만들어 놓은 것이다.

객체 리터럴을 사용한 모듈 패턴: 객체 리터럴은 모듈 패턴이기도 하며, 하나의 객체라는 점에서 싱글톤 패턴이라고도 할 수 있다. 동일한 코드를 어떠한 관점에서 보느냐에 따라 다양한 패턴이 될 수 있다. 객체 리터럴은 간단하지만 모든 속성이 공개되어있다는 단점이 있다. 독립된 모듈은 자체적으로 필요한 내부 변수 및 내부 함수를 모두 갖고 있어야 하므로 클로저를 이용해야 한다.

ES Module: ES6에 도입된 모듈 시스템.
import, export를 사용해 분리된 자바스크립트 파일끼리 서로 접근할 수 있다. ES 는 프로그래밍 언어가 아닌 스크립트 언어들에 대한 표준, 규격입니다.

유틸리티 패키지: Utility 모듈은 node.js의 보조적인 기능 중 유용한 기능만을 모아놓은 모듈입니다. 모든 메소드는 API 문서에서 볼 수 있습니다.

인터페이스: 인터페이스는 변수나 함수, 그리고 클래스가 만족해야하는 최소 규격을 지정할 수 있게 해주는 도구이다.
그래서 사용자 정의 자료형으로도 사용할 수 있다.

entry porint: 엔트리 포인트(entry point) 또는 진입점(進入點)은 제어가 운영 체제에서 컴퓨터 프로그램으로 이동하는 것을 말하며, 프로세서는 프로그램이나 코드에 진입해서 실행을 시작한다.

require: 메서드는 외부 모듈을 가져올 때 사용

모듈: 노드에서 모듈이라는 개념은 노드로 개발한 애플리케이션을 이루는 기본 조각이라고 할 수 있습니다.
독립된 기능을 하는 함수나 변수들의 집합이라 할 수 있고, 모듈 자체가 하나의 프로그램이면서 다른 프로그램의 부품으로 사용하여 재사용에 용이하다. 모듈은 NodeJS에서 제공하는 것이 있고, 누군가가 만들어 놓은 것도 있고 자신이 직접 만들어서 사용할 수도 있다. 모듈을 크게 보자면 2가지로 나눌 수 있다.

Es와 Commonjs: ESM와 CJS는 호환이 안된다. ESM에서 CJS를 default import하거나 CJS에서 ESM을 require로 가져오는 방법만이 가능하지만 이조차도 많은 boilerplate와 번들러가 필요하며 순서가 보장되지 않는다.

=== -> 동치연산자
```