# Package entry points

```jsx
In a package’s package.json file, two fields can 
define entry points for a package: "main" and 
"exports".
```

> 패키지의 package.json 파일에서 "main" 및 "exports"라는 두 개의 필드가 패키지의 entry points을 정의할 수 있습니다.
> 

```jsx
The "main" field is supported in all versions of 
Node.js, but its capabilities are limited: it only 
defines the main entry point of the package.
```

> "main" 필드는 모든 버전의 Node.js에서 지원되지만 그 기능은 제한적이다.
> 

```jsx
The "exports" field provides an alternative to 
"main" where the package main entry point can be 
defined while also encapsulating the package, 
preventing any other entry points besides those 
defined in "exports".
```

> "exports" 필드는 패키지를 캡슐화하면서 정의될 수 있는 "main"에 대한 대안을 제공하여 "exports"에 정의된 것 이외의 다른 엔트리 포인트를 방지한다.
> 

```jsx
This encapsulation allows module authors to define 
a public interface for their package.
```

> 이 캡슐화를 통해 모듈 작성자는 패키지에 대한 공용 인터페이스를 정의할 수 있습니다.
> 

```jsx
If both "exports" and "main" are defined, the 
"exports" field takes precedence over "main".
```

> "exports"와 "main"이 모두 정의된 경우 "exports" 필드가 "main"보다 우선적입니다.
> 

```jsx
"exports" are not specific to ES modules or 
CommonJS; "main" is overridden by "exports" if it 
exists.
```

> "exports"는 ES모듈이나 CommonJS에 한정되지 않고, "main"은 존재하는 경우 "exports"에 의해 무시(재정의)됩니다.
> 

```jsx
As such "main" cannot be used as a fallback for 
CommonJS but it can be used as a fallback for 
legacy versions of Node.js that do not support the
"exports" field.
```

> 이러한 "main"은 CommonJS의 대체 수단으로 사용할 수 없지만 "exports" 필드를 지원하지 않는 Node.js의 레거시 버전에 대한 대체 수단으로 사용할 수 있습니다.
> 

```jsx
Conditional exports can be used within "exports" to 
define different package entry points per 
environment, including whether the package is 
referenced via require or via import.
```

> 조건부 exports는 "exports" 내에서 패키지가 required 또는 import를 통해 참조되는지를 포함하여 환경별로 다른 패키지 entry point를 정의하기 위해 사용될 수 있다.
> 

```jsx
For more information about supporting both CommonJS 
and ES Modules in a single package please consult 
the dual CommonJS/ES module packages section.
```

> 단일 패키지로 CommonJS 및 ES 모듈을 지원하는 방법에 대한 자세한 내용은 듀얼 CommonJS/ES 모듈 패키지 섹션을 참조하십시오.
> 

```jsx
Warning: Introducing the "exports" field prevents 
consumers of a package from using any entry points 
that are not defined, including the package.json 
(e.g. require('your-package/package.json').
```

> 경고: "exports" 필드를 도입하면 패키지 소비자가 package.json(예: require('your-package/package.json')을 포함하여 정의되지 않은 entry points을 사용할 수 없습니다.
> 

```jsx
This will likely be a breaking change.
```

> 이것은 아마도 주요 변경 사항이 될 것입니다.
> 

```jsx
To make the introduction of "exports" non-breaking, 
ensure that every previously supported entry point 
is exported.
```

> "exports"를 중단 없이 사용하려면 이전에 지원되는 모든 entry point를 내보내야 합니다.
> 

```jsx
It is best to explicitly specify entry points so 
that the package’s public API is well-defined.
```

> 패키지의 공개 API가 잘 정의되도록 entry points을 명시적으로 지정하는 것이 가장 좋습니다.이것은 아마도 주요 변경 사항이 될 것입니다.
> 

```jsx
For example, a project that previous exported main, 
lib, feature, and the package.json could use the 
following package.exports:
```

> 예를 들어 이전에 main, lib 기능 및 package.json 등 내보낸 프로젝트는 다음 package.exports를 사용할 수 있습니다.
> 

```jsx
Alternatively a project could choose to export 
entire folders:
```

> 또는 프로젝트에서 전체 폴더를 내보내도록 선택할 수 있습니다.
> 

```jsx
As a last resort, package encapsulation can be 
disabled entirely by creating an export for the root 
of the package "./*": "./*".
```

> 최후의 수단으로 패키지 "./*": "./*"의 루트에 대한 내보내기를 생성하여 패키지 캡슐화를 완전히 비활성화할 수 있습니다.
> 

```jsx
This exposes every file in the package at the cost 
of disabling the encapsulation and potential tooling
benefits this provides.
```

> 이것은 캡슐화를 비활성화하고 이것이 제공하는 패키지의 내부 장점을 희생시키면서 패키지의 모든 파일을 노출합니다.
> 

```jsx
As the ES Module loader in Node.js enforces the use 
of the full specifier path, exporting the root rather
than being explicit about entry is less expressive 
than either of the prior examples.
```

> Node.js의 ES 모듈 로더는 전체 지정자 경로의 사용을 강제하기 때문에 항목에 대해 명시적인 것보다 루트를 내보내는 것은 이전 예보다 표현력이 떨어집니다.
> 

```jsx
Not only is encapsulation lost but module consumers 
are unable to import feature from 'my-mod/feature' 
as they need to provide the full path import feature 
from 'my-mod/feature/index.js.
```

> 캡슐화가 손실될 뿐만 아니라 모듈 소비자는 'my-mod/feature/index.js'에서 전체 경로 가져오기 기능을 제공해야 하므로 'my-mod/feature'에서 기능을 가져올 수 없습니다.
> 

```jsx
entry porint: 엔트리 포인트(entry point) 또는 진입점(進入點)은 제어가 운영 체제에서 컴퓨터 프로그램으로 이동하는 것을 말하며, 프로세서는 프로그램이나 코드에 진입해서 실행을 시작한다. 

모듈: 모듈이란 관련된 객체들의 집합소.

어떠한 기능을 수행하기 위해 함수 또는 객체들을 만들어 놨으면, 그걸 한 .js의 파일에 써놓기엔 가독성이나 유지보수가 좋지 않아서 관련 함수 또는 객체들을 .js파일별로 따로 모아놓은것들을 모듈이라고 생각하면 된다.

exports module.exports 차이: exports객체와 module.exports객체는 동일하며 exports 가 module.exports객체를 call by reference 방식으로 바라보고 있으며, 최종적으로 리턴값은 module.exports 라는 것이다.

캡슐화: 객체의 속성(data fields)과 행위(메서드, methods)를 하나로 묶고 실제 구현 내용 일부를 내부에 감추어 은닉한다. 내부에 감추는 방법으로는 언어적 측면에서 접근지정자를 두어 은닉의 정도를 기술하여 구현한다. 은닉의 정도를 접근지정자로 기술하고 해당 영역에 들어가는 속성이나 메서드를 제한하면 된다. 접근지정자에 의해 제한된 멤버들은 컴파일러에 의해 판단된다.

ES모듈: ES6에 도입된 모듈 시스템.
import, export를 사용해 분리된 자바스크립트 파일끼리 서로 접근할 수 있다.

ES모듈을 사용하는 이유: 초기 자바스크립트는 독립적인 작업을 수행하며 큰 스크립트가 필요하지 않았다. jQuery가 생겨나고 어플리케이션의 규모가 커지면서 script파일을 나누기 시작했고, 파일간의 변수, 함수 등을 전달하고 받는 방법이 필요했다.

 ES 모듈화 장점: 
import - export의 명시적 관계로, 하나의 모듈이 제거되면 어떤 모듈이 손상되었는지 알 수 있다. 즉, 의존성 파악에 용이하다.(A가 import B를 하고 있을 때, B가 사라지거나 오류가 생기면 not found B 에러가 뜨는 등)

코드들을 각각 독립적으로 작동할 수 있는 단위로 나누기 수월하다. 이는 모듈을 재사용함으로써 다양한 종류의 어플리케이션을 만들 수도 있다.

import - export로 관계되지 않은 모듈간의 오염은 일어나지 않는다.

CommonJS: JavaScript를 브라우저에서뿐만 아니라, 서버사이드 애플리케이션이나 데스크톱 애플리케이션에서도 사용하려고 조직한 자발적 워킹 그룹이다. CommonJS의 'Common'은 JavaScript를 브라우저에서만 사용하는 언어가 아닌 일반적인 범용 언어로 사용할 수 있도록 하겠다는 의지를 나타내고 있는 것이라고 이해할 수 있다.

레거시 버전: Legacy 버전은 IE6, IE7, IE8, IE9, IE10에서 모두 사용가능하지만 최신판은 아닌 것이다. 만약 플러그인을 사용하는 홈페이지가 접속 연령대가 다양하여 예전 브라우저도 지원을 해야 한다면 Legacy버전을 쓸 수밖에 없다.

레거시: 유산이라는 뜻의 영단어. 현재까지 남아 사용되고 있거나 현재의 체계에 영향을 미치는 과거의 체계를 뜻한다. 가족이나 혈통이 남긴 유산이란 뜻으로도 많이 쓰인다

레거시 시스템: 낡은 기술이나 방법론, 컴퓨터 시스템, 소프트웨어 등을 말한다. 이는 현대까지도 남아 쓰이는 기술을 부르는 말일 수도 있지만, 더 이상 쓰이지 않더라도 현대의 기술에 영향을 주는 경우도 포함한다.

API: 애플리케이션 프로그래밍 인터페이스, 응용 프로그램 프로그래밍 인터페이스)는 컴퓨터나 컴퓨터 프로그램 사이의 연결이다. 일종의 소프트웨어 인터페이스이며 다른 종류의 소프트웨어에 서비스를 제공한다.
```