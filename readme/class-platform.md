# Class Platform

#### Introduction

This class provides platform-level operations, and typically requires presenting system security credentials when invoked. These security credentials are issued to the UI after the client account is unlocked with a passcode. The UI needs to retain these security credentials throughout its entire lifecycle, and they must be presented when invoking this class.

**Class platform**

```typescript
import { platform， type_platformStatus } from 'API/platfrom'

const [platformStatus, setPlatformStatus] = useState<type_platformStatus>('')
const [workerLoading, setWorkerLoading] = useState（0)

const conetPlatform = new platform(setPlatformStatus, setWorkerLoading)

```

**new platform(platformStatus, workerLoading)**

* setPlatformStatus: [React.Dispatch](https://react-redux.js.org/api/hooks)\<React.SetStateAction\<type\_platformStatus>>
* type\_platformStatus: 'LOCKED'|'UNLOCKED'|'NONE'
* setWorkerLoading: React.Dispatch\<React.SetStateAction\<number>>: from0\~100
* Returns:  Instance of [class](https://www.typescriptlang.org/docs/handbook/2/classes.html) platform.

Creates a new instance of platform. Monitor the percentage of backend processes being loaded by **setWorkerLoading**, Show client status when loading is complete by **setPlatformStatus.**



**platform.createAccount(passcode)**

* **Returns:** Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>
* **Return resolve**: 12 words Secret Recovery Phrase (SRP) split by space, zero length string (create account was fail)
* **Return reject**: Never.
* **passcode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5)

This function only available when platform.passcode is "NONE"



**platform.testPasscode(passcode)**

* **Returns:** Promise\<boolean>
* **Return resolve**:  when true, fail when false.
* **Return reject**: Never.
* **passcode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5)

Class platform will get authorization key from backend which can access user private data after passcode is success.



**platform.showSRP()**

* **Returns:** Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) \[]>
* **Return resolve**: 12 words Secret Recovery Phrase (SRP) or zero length (unavailable)
* **return reject**: Never.
* **Require:** Class platform has complete authorization.



**platform.currentProfile()**

* **Returns:** Promise\<profile>
* **Return resolve**: profile or null (unavailable)
* **return reject**: Never.
* **Require:** Class platform has complete authorization.



**platform.deleteAccount()**

* **Returns**: Promise\<boolean>
* **Return resolve**: **true**: success. **false**: fail
* **Return reject**: Never.





