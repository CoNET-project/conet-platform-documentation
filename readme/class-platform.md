# Class Platform

#### Introduction

This class provides platform-level operations, and typically requires presenting system security credentials when invoked. These security credentials are issued to the UI after the client account is unlocked with a passcode. The UI needs to retain these security credentials throughout its entire lifecycle, and they must be presented when invoking this class.

**Class platform**

```typescript
import { platform } from 'API/platfrom'
```

**new platform()**

Creates a new instance of **platform**.



**platform.passcode**

CONET Platform status.

**LOCKED**: user need unlock first before use the platform function.

**UNLOCKED**: the platform is ready.

**NONE**: CONET Platform is the first time to launched.



**platform.create()**



\


