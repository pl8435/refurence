# Writing dual packages while avoiding or minimizing hazards

```jsx
First, the hazard described in the previous section occurs 
when a package contains both CommonJS and ES module 
sources and both sources are provided for use in Node.js, 
either via separate main entry points or exported paths.
```

> 첫째, 이전 섹션에서 설명한 위험은 패키지에 CommonJS 및 ES 모듈 소스가 모두 포함되어 있고 두 소스가 별도의 기본 진입점 또는 내보낸 경로를 통해 Node.js에서 사용하도록 제공될 때 발생합니다.
> 

```jsx
A package might instead be written where any version of 
Node.js receives only CommonJS sources, and any separate 
ES module sources the package might contain are intended 
only for other environments such as browsers.
```

> Node.js의 모든 버전이 CommonJS 소스만 수신하는 경우 패키지가 대신 작성될 수 있습니다. 패키지에 포함될 수 있는 별도의 ES 모듈 소스는 브라우저와 같은 다른 환경에만 사용됩니다.
> 

```jsx
Such a package would be usable by any version of Node.js, 
since import can refer to CommonJS files; but it would not 
provide any of the advantages of using ES module syntax.
```

> import는 CommonJS 파일을 참조할 수 있기 때문에 이러한 패키지는 모든 버전의 Node.js에서 사용할 수 있습니다. 그러나 ES 모듈 구문을 사용하는 이점은 제공하지 않습니다.
> 

```jsx
A package might also switch from CommonJS to ES module 
syntax in a breaking change version bump.
```

> 패키지는 브레이킹 체인지 버전 범프를 통해 CommonJS에서 ES 모듈 구문으로 전환될 수도 있습니다.
> 

```jsx
This has the disadvantage that the newest version of the
 package would only be usable in ES module-supporting 
versions of Node.js.
```

> 최신 버전의 패키지는 ES 모듈 지원 버전의 Node.js에서만 사용할 수 있다는 단점이 있습니다.
> 

```jsx
Every pattern has tradeoffs, but there are two broad 
approaches that satisfy the following conditions:
```

> 모든 패턴에는 장단점이 있지만 다음 조건을 충족하는 두 가지 광범위한 접근 방식이 있습니다.
> 

```jsx
1. The package is usable via both require and import.
```

> 1.  패키지는 require와 import를 통해 사용할 수 있습니다.
> 

```jsx
2.The package is usable in both current Node.js and older 
versions of Node.js that lack support for ES modules.
```

> 2.  이 패키지는 현재 Node.js 및 ES 모듈을 지원하지 않는 이전 버전의 Node.js에서 모두 사용할 수 있습니다.
> 

```jsx
3.The package main entry point, e.g. 'pkg' can be used by 
both require to resolve to a CommonJS file and by import 
to resolve to an ES module file. (And likewise for 
exported paths, e.g. 'pkg/feature'.)
```

> 3.  패키지 주요 진입점(예: 'pkg')은 CommonJS 파일을 확인하기 위해 필요로 하고 ES 모듈 파일은 import을 통해 확인 할 수 있습니다.(내보낸 경로의 경우에도 마찬가지입니다. 예: 'pkg/feature'.)
> 

```jsx
4.The package provides named exports, e.g. import { name } 
from 'pkg' rather than import pkg from 'pkg'; pkg.name.
```

> 4. 이 패키지는 명명된 엑스포트를 제공합니다(예: 'pkg'에서 pkg를 가져오는 대신 'pkg'에서 { name } 가져오기). [pkg.name](http://pkg.name/)
> 

```jsx
5.The package is potentially usable in other ES module 
environments such as browsers.
```

> 5.  이 패키지는 브라우저와 같은 다른 ES 모듈 환경에서 잠재적으로 사용할 수 있습니다.
> 

```jsx
6.The hazards described in the previous section are 
avoided or minimized.
```

> 6.  이전 섹션에서 설명한 위험을 피하거나 최소화합니다.
>