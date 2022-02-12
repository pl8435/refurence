# Dual CommonJS/ES module packages

```jsx
Prior to the introduction of support for ES modules in 
Node.js, it was a common pattern for package authors to 
include both CommonJS and ES module JavaScript sources in 
their package, with package.json "main" specifying the 
CommonJS entry point and package.json "module" specifying 
the ES module entry point.
```

> Node.js에서 ES 모듈에 대한 지원을 도입하기 전에는 패키지 작성자가 CommonJS 진입점 및 패키지를 지정하는 package.json "main"과 함께 패키지에 CommonJS 및 ES 모듈 JavaScript 소스를 모두 포함하는 것이 일반적인 패턴이었습니다. ES 모듈 진입점을 지정하는 json "module".
> 

```jsx
This enabled Node.js to run the CommonJS entry point while 
build tools such as bundlers used the ES module entry 
point, since Node.js ignored (and still ignores) the 
top-level "module" field.
```

> 이것은 Node.js가 최상위 "모듈" 필드를 무시(그리고 여전히 무시)하기 때문에 번들과 같은 빌드 도구가 ES 모듈 진입점을 사용하는 동안 Node.js가 CommonJS 진입점을 실행할 수 있도록 합니다.
> 

```jsx
Node.js can now run ES module entry points, and a package 
can contain both CommonJS and ES module entry points 
(either via separate specifiers such as 'pkg' and 
'pkg/es-module', or both at the same specifier via 
Conditional exports).
```

> 이제 Node.js는 ES 모듈 진입점을 실행할 수 있으며 패키지는 CommonJS 및 ES 모듈 진입점을 모두 포함할 수 있습니다('pkg' 및 'pkg/es-module'과 같은 별도의 지정자 또는 조건부 내보내기를 통해 동일한 지정자를 가질 수 있습니다). (뭘 하든 같은 패키지로 지정)
> 

```jsx
Unlike in the scenario where "module" is only used by 
bundlers, or ES module files are transpiled into CommonJS 
on the fly before evaluation by Node.js, the files 
referenced by the ES module entry point are evaluated as 
ES modules.
```

> "module"이 번들에서만 사용되거나 Node.js에서 평가되기 전에 ES 모듈 파일이 CommonJS로 즉시 변환되는 시나리오와 달리 ES 모듈 진입점에서 참조하는 파일은 ES 모듈로 평가됩니다.
> 

> "module"이 번들에서만 사용되거나 Node.js에서 평가되기 전에 ES 모듈 파일이 CommonJS로 즉시 변환되는 시나리오와 달리 ES 모듈 진입점에서 참조하는 파일은 ES 모듈로 평가됩니다.
>