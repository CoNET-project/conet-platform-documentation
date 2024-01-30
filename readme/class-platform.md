# Class Platform

#### Introduction

This class provides platform-level operations, and typically requires presenting system security credentials when invoked. These security credentials are issued to the UI after the client account is unlocked with a passcode. The UI needs to retain these security credentials throughout its entire lifecycle, and they must be presented when invoking this class.

**Class platform**

```typescript
import { platform } from 'API/platfrom'
```



**new platform()**

* Returns:  Instance of [class](https://www.typescriptlang.org/docs/handbook/2/classes.html) platform.

Creates a new instance of platform.



**platform.passcode**&#x20;

* <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> READ ONLY. CONET Platform status.

**LOCKED**: user need unlock first before use the platform function.

**UNLOCKED**: the platform is ready.

**NONE**: CONET Platform is the first time to launched.

**Empty string**

```typescript
typeof platform.passcode === 'string' && 
    ( platform.passcode === '' || 
    !platform.passcode.length )
```

Class platform is initialization failed. Daemon worker hasn't ready or initialization failed.



**platform.createAccount(passcode)**

* Returns: Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) \[]>
* return resolve: 12 words Secret Recovery Phrase (SRP) or zero length (create account was fail)
* return reject: Never.
* passcode <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> length > 5

This function only available when platform.passcode is "NONE"



**platform.showSRP()**

* Returns: Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) \[]>
* return resolve: 12 words Secret Recovery Phrase (SRP) or zero length (unavailable)
* return reject: Never.



**platform.deleteAccount()**

Returns: Promise\<boolean>

return resolve: true: success. false: fail



