
## Installation

### add dependency to your build.gradle file

``` kotlin
implementation("mu.mips:android_sdk:0.2.3")
```
##### or

``` groovy
implementation 'mu.mips:android_sdk:0.2.3'
```

##### or 

#### [visit maven central](https://central.sonatype.com/artifact/mu.mips/android_sdk)


## Usages (Kotlin)

1. create instance of Merchant details (provided by MIPS admin)
``` kotlin 
val detail = MerchantDetails(  
    sIdMerchant = "XXXXXXXXXX",  
    salt = "XXXXXXXXXX",  
    sCipherKey = "XXXXXXXXXX",  
    id_entity = "XXXXXXXXXX",  
    id_operator = "XXXXXXXXXX",  
    operator_password = "XXXXXXXXXX"  
)
```
2. create instance of MerchantCredentials
``` kotlin 
val credential = MerchantCredentials(  
    username = "XXXXXXXXXX",  
    password = "XXXXXXXXXX"
)
```

3. create instance of MerchantCredentials
``` kotlin
val amount = mu.mips.mips_payment_sdk.Models.Amount(  
    Currency.MAURITIAN_RUPEE,  
    100  
)
```

4. get order ID
``` kotlin
val orderID = UUID.randomUUID().toString()
```

5. create a fragment of type MIPS_Payment_Fragent  

```kotlin
var paymentFrag: MIPS_Payment_Fragent = 
		MIPS_Payment_Fragent.getInstance(  
		    detail ,  
		    credential ,  
		    amount ,  
		    orderID ,  
		    successCallback = { mode ->  
		        showSuccessScreen()  
		    } ,  
		    failureHandler = {
		        showFailureScreen()  
		    }  
		)
```

6. show the payment fragment to process payment further

```kotlin
val ft = supportFragmentManager.beginTransaction()  
ft.add(R.id.CONTAINER_ID, paymentFrag).commit()
```
7.  optionally you can also force check for success payment status without waiting for callback by calling forceCheckStatus function available on fragment class
``` kotlin
paymentFrag.forceCheckStatus() 
// it will call successCallBack labda function passed to fragment constructor if payment is already done
```

## Usages (Java)

1. create instance of Merchant details (provided by MIPS admin)
``` java 
MerchantDetails detail = new MerchantDetails(
    "XXXXXXXXXX", 
    "XXXXXXXXXX", 
    "XXXXXXXXXX", 
    "XXXXXXXXXX", 
    "XXXXXXXXXX", 
    "XXXXXXXXXX"  
);
```
2. create instance of MerchantCredentials
``` java 
MerchantCredentials credential = new MerchantCredentials(
    "XXXXXXXXXX", 
    "XXXXXXXXXX"  
);
```

3. create instance of MerchantCredentials
``` java
Amount amount = new Amount(
	Currency.MAURITIAN_RUPEE, 
	100 
);
```

4. get order ID
``` java
String orderID = UUID.randomUUID().toString();
```

5. create a fragment of type MIPS_Payment_Fragent  

```java
MIPS_Payment_Fragent paymentFrag = 

	MIPS_Payment_Fragent.Companion.getInstance(  
	        detail,  
	        credential,  
	        amount,  
	        orderID,  
	        paymentMode -> {   // success handler
	            PaymentMode mode = paymentMode;  
	            showSuccessScreen();  
	            return Unit.INSTANCE;  
	        },  
	        () -> {  // failuer handler
	            showFailureScreen();  
	            return Unit.INSTANCE;  
	        }  
);
```

6. show the payment fragment to process payment further

```java
FragmentTransaction ft = getSupportFragmentManager().beginTransaction();  
ft.add(R.id.CONTAINER_ID, paymentFrag).commit();

```
7.  optionally you can also force check for success payment status without waiting for callback by calling forceCheckStatus function available on fragment class
``` java
paymentFrag.forceCheckStatus() 
// it will call successCallBack labda function passed to fragment constructor if payment is already done
```

