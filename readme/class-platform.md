# Class Platform

#### Introduction

This class provides platform-level operations, and typically requires presenting system security credentials when invoked. These security credentials are issued to the UI after the client account is unlocked with a passcode. The UI needs to retain these security credentials throughout its entire lifecycle, and they must be presented when invoking this class.

**Class platform**

<pre class="language-typescript"><code class="lang-typescript"><strong>import { platform， type_platformStatus } from 'API/platfrom'
</strong>
const [platformStatus, setPlatformStatus] = useState&#x3C;type_platformStatus>('')
const [workerLoading, setWorkerLoading] = useState（0)

const conetPlatform = new platform(setPlatformStatus, setWorkerLoading)
</code></pre>

**Type profile**

```typescript
interface pgpKey {
	privateKeyArmor: string
	publicKeyArmor: string
}
interface token {
	balance: string
	name: string
	symbol: string
	erc20Address: string
	history: tokenHistory[]
}
interface profile {
	isPrimary: boolean			//	true: current profile
	referrer?: referrer			//	referrer only in the first profile. 
	keyID: string 				//	Wallet Address
	pgpKey: pgpKey				//
	privateKeyArmor: string			//	Wallet private key
	tokens: token[]
	data?: any				//	UI custom data, like nickname
	
}
```

**new platform(platformStatus, workerLoading)**

* setPlatformStatus: [React.Dispatch](https://react-redux.js.org/api/hooks)\<React.SetStateAction\<type\_platformStatus>>
* type\_platformStatus: 'LOCKED'|'UNLOCKED'|'NONE'
* setWorkerLoading: React.Dispatch\<React.SetStateAction\<number>>: from0\~100
* Returns:  Instance of [class](https://www.typescriptlang.org/docs/handbook/2/classes.html) platform.

Creates a new instance of platform. Monitor the percentage of backend processes being loaded by **setWorkerLoading**, Show client status when loading is complete by **setPlatformStatus.**

### Security credentials required functions

**platform.createAccount(passcode)**

* **Returns:** Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>
* **Return resolve**: 12 words Secret Recovery Phrase (SRP) split by space, zero length string (create account was fail)
* **Return reject**: Never.
* **passcode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5)

This function only available when **platformStatus** is "NONE"



**platform.testPasscode(passcode)**

* **Returns:** Promise<\[passcodeStatus: boolean, authorizationKey: string]>
* **Return resolve**:  Unlock wallet success when passcodeStatus is true, return **authorizationKey**. Unlock wallet fail when passcodeStatus was false.
* **Return reject**: Never.
* **passcode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5)

**platformStatus** will be update to **UNLOCKED** when passcode success.

Class platform will get authorization key from backend which can access user private data after passcode is success.&#x20;



**platform.resetPasscode(oldPasscode, newPasscode)**

* **Returns:** Promise<\[passcodeStatus: boolean, authorizationKey: string]>
* **Return resolve**:  Unlock wallet success when reset passcode was down, return **authorizationKey**. Unlock wallet fail when passcodeStatus was false.
* **Return reject**: Never.
* **oldPasscode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5)
* **newPasscode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5)



**platform.recoverAccount(SRP, passcode)**

* **Returns:** Promise\<authorizationKey: string>
* **Return resolve**:  Return **authorizationKey** when recover Account from SRP, or null when recover fail.&#x20;
* **Return reject**: Never.
* **SRP** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>  12 words Secret Recovery Phrase (SRP) split by space.
* **passcode** <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> (length > 5) The new passcode for securus account.



**platform.showSRP(**authorizationKey**)**

* **authorizationKey**<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> The access authorization which return from success testPasscode.
* **Returns:** Promise<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>
* **Return resolve**: 12 words Secret Recovery Phrase (SRP) split by space or zero length string (unavailable)
* **return reject**: Never.
* **Require:** Class platform has complete authorization.



**platform.getAllProfiles(**authorizationKey**)**

* **authorizationKey**<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>  The access authorization which return from success testPasscode.
* **Returns:** Promise\<profile\[]>
* **Return resolve**: All profiles or null array (unavailable)
* **return reject**: Never.
* **Require:** Class platform has complete authorization.



**platform.importWallet(**authorizationKey, privateKey, data**)**

* **authorizationKey**<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>  The access authorization which return from success testPasscode.
* **privateKey**<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>  The private key.
* **data** \<any> UI custom data. example want put a "import" TAG.
* **Returns:** Promise\<profile\[]>
* **Return resolve**: All profiles or null array (when private key or authorizationKey is illegal.)
* **Return reject**: Never.
* **Require:** Class platform has complete authorization.



**platform.updateProfile(**authorizationKey, profile**)**

* **authorizationKey**<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>  The access authorization which return from success testPasscode.
* profile\<profile> Include UI custom data.
* **Returns:** Promise\<profile\[]>
* **Return resolve**: All profiles or null array (when profile or authorizationKey is illegal.)
* **Return reject**: Never.
* **Require:** Class platform has complete authorization.



**platform.addProfile(**authorizationKey, data**)**

* **authorizationKey**<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>  The access authorization which return from success testPasscode.
* **data** \<any> UI custom data. example want put a "import" TAG.
* **Returns:** Promise\<profile\[]>
* **Return resolve**: All profiles or null array (when authorizationKey is illegal.)
* **Return reject**: Never.
* **Require:** Class platform has complete authorization.



**platform.purchaseNodes(**authorizationKey, nodes, total: number, currency, purchasePrivacyKey, status**)**

* **authorizationKey**<[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)>  The access authorization which return from success testPasscode.
* **nodes\<number>:** The total number of purchase nodes.
* **currency\<string>**: The used currency name.
* **purchasePrivacyKey\<string>**: Use to sign purchase.
* status\<React.Dispatch\<React.SetStateAction\<purchaseStatus>>>: Hooks to return status.

```typescript
type purchaseStatus = 
    'approving'|'approve fail'|        //    USDT, USDB approve process
    'transferring'|'transfer fail'|    //    ETH, bETH, BNB transfer process
    'Completing purchase'|            //    Waiting CONET complete purchase process
    'purchase fail'｜                //    CONET refuses transaction
    'success'                        //    purchase success
    'Getting node information'        //    get information from CONET Holesky
    'Done'                            //    
    
```

### No security credentials required functions

**platform.CONET**Faucet(privateKey)

* **Returns**: Promise\<boolean> True: success, False: fail. (each 24 hours can request once only.)



**platform.getRefereesList(**wallet\_public\_key**)**

* **Returns:** Promise\<refereesTree\[]>

```typescript
//    refereesTree result examples 0x04441E4BC3A8842473Fe974DB4351f0b126940be
refereesTree: {
    '0x4fa1FC4a2a96D77E8521628268631F735E2CcBee':[
        {
            '0xDBaa41dd7CABE1D5Ca41d38E8F768f94D531d85A': 
                ['0xc9043f661ADddCAF902d45D220e7aea38920d188'] 
        }
    ]
}
```

* wallet\_public\_key <[string](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)> profile.keyID

Return referees tree array.

**platform.getAssetsPrice()**

* **Returns:** Promise\<price\[]>

```typescript
Price = {
    BNB: {USD: number},
    ETH: {USD: number},
    USDT: {USD: number}
}
```

* **Return reject**: Never.



**platform.deleteAccount()**

* **Returns**: Promise\<boolean>
* **Return resolve**: **true**: success. **false**: fail
* **Return reject**: Never.





