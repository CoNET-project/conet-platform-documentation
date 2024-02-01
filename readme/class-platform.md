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



**platform.passcode()**

* **Returns**: Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>&#x20;
* **Return resolve**: LOCKED | UNLOCKED | NONE | ''
* **Return reject**: Never.
* **LOCKED**: user need unlock first before use the platform function.
* **UNLOCKED**: the platform is ready.
* **NONE**: CONET Platform is the first time to launched.
*   **Empty string:** Class platform is initialization failed. Daemon worker hasn't ready or initialization failed.

    ```typescript
        typeof platform.passcode === 'string' && ( platform.passcode === '' || 
        !platform.passcode.length )
    ```

Platform status.



**platform.createAccount(passcode)**

* **Returns:** Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) \[]>
* **Return resolve**: 12 words Secret Recovery Phrase (SRP) or zero length (create account was fail)
* **Return reject**: Never.
* **passcode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5)

This function only available when platform.passcode is "NONE"



**platform.showSRP()**

* **Returns:** Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) \[]>
* **Return resolve**: 12 words Secret Recovery Phrase (SRP) or zero length (unavailable)
* **return reject**: Never.



**platform.deleteAccount()**

* **Returns**: Promise\<boolean>
* **Return resolve**: **true**: success. **false**: fail
* **Return reject**: Never.





