# Faspay SDK CREDIT

this SDK 


for import

```php
require_once '../../credit/entity/payment/FaspayPaymentCreditWrapperProd.php';
require_once '../../credit/entity/payment/FaspayPaymentCredit.php';
require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditTransactionData.php';
require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditShopperData.php';
require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditConfigApp.php';
require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditBillData.php';


require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditShippingdata.php';
require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditItemData.php';
require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditDomicileData.php';
require_once '../../credit/entity/payment/wrapper/FaspayPaymentCreditCardData.php';

require_once '../../credit/entity/inquiry/InquiryRequestCredit.php';
require_once '../../credit/entity/inquiry/InquiryRequestCreditWrapper.php';
require_once '../../credit/entity/inquiry/InquiryResponseCredit.php';
require_once '../../credit/FaspayConfigCreditProd.php';

require_once '../../credit/FaspayUserCredit.php';
require_once '../../credit/TestUser2.php';
require_once '../../credit/service/FaspayCreditService.php';
require_once '../../credit/service/FaspayCreditServiceImpl.php';

```



# User Object

just like debit payment, this SDK needs user object, 

```php
    class TestProdUser extends FaspayUserCredit{
        function __construct() {
            $this->setMerchantId("faspay");
            $this->setPass("abcde");
        }

    }

```



# Faspay Credit Create Payment

just like debit function, this function create the payment but user must fill the form of html 

```php
    //sample code
        //create the items first
        $item = array();
        array_push($item, "Racun tikus");
        array_push($item, "Bubur ayam");
        array_push($item, "Pil KB");

                //from previous code 
                $usr = new TestProdUser();
                
```

create credit card data;
```php
$ccdata = new FaspayPaymentCreditCardData()
```

create domicile data
```php
$domData = new FaspayPaymentCreditDomicileData();
```
create item wrapper data
```php
$itemData = new FaspayPaymentCreditItemData($item)
```

create shipping data
```php
            //$shipping_address, 
            //$shipping_address_city, 
            //$shipping_address_region, 
            //$shipping_address_state, 
            //$shipping_address_poscode, 
            //$shipping_address_country_code, 
            //$shippingcost
$shipData = new FaspayPaymentCreditShippingdata("addr", "city", "region", "state", "poscode", "ID", 100000);
```
create bill data

```php
//$billing_address
// $billing_address_city
// $billing_address_region
// $billing_address_state
// $billing_address_poscode
/ $billing_address_country_code
$billData = new FaspayPaymentCreditBillData("adr", "city", "region", "state", "poscode", "ID");
```
create the config 

```php
//FaspayPaymentCredit::RESPONSE_TYPE_POST see #https://faspay.co.id/docs/index-business.html?json#request-parameter

new FaspayPaymentCreditConfigApp(FaspayPaymentCredit::RESPONSE_TYPE_POST, "http://<<URL CALLBACK>>")
```


create shopper data
```php
//$custname, $custemail
// $shopper_ip
// $description
// $cardno
// $cardname
// $cardtype
// $expirymonth
// $expiryyear
// $phone_no
new FaspayPaymentCreditShopperData("ha", "ha@ha.com",
                        "192.168.100.1","desc", "9612361233123", "Test user", 
                        FaspayPaymentCredit::CARD_TYPE_AMEX, 10, "2020", "081236125123");
```
this example will show the HTML of your browser via desktop platform, in android you can use WebView

# Faspay Credit Capture Payment
```java
    String html = new CaptureRequestWrapperProd(new TestUserBaruCredit(), "c0f4dbe47d27490e81a03ee771be6b47", "110B90DB-DA6C-4FEC-8ACD-C1DBF78A2E61", 10000, "ha", "haha@haha.com", "ddddd ", "<<URL NOTIFY>>").generateHtml();
        try {
            File temp = File.createTempFile(UUID.randomUUID().toString(), ".html");

            FileOutputStream fos = new FileOutputStream(temp);
            fos.write(html.getBytes());
            fos.flush();
            fos.close();
            System.out.println();
            System.out.println(temp.getAbsolutePath());
           // openFile(temp);
        } catch (Exception e) {
            e.printStackTrace();
        }
```

this example will show the HTML of your browser via desktop platform, in android you can use WebView


# Faspay Credit Inquiry  Payment

this example will generate the HTML of your browser via desktop platform, in android you can use WebView

```java
    FaspayConfigCredit conf = new FaspayConfigCreditProd();
    FaspayUserCredit credit = new TestUserBaruCredit();
    InquiryRequestCredit d = new InquiryRequestCreditWrapper(conf, credit, "e5f95232e08446cabda1b10ce6deb579", 10000);
    d.generateHtml()
```



# Faspay Credit Refund  Payment
this example will generate the HTML of your browser via desktop platform, in android you can use WebView
```java
String html = new RefundRequestWrapperProd(new TetsUser2(), "64ddf6a2dc1347dca59c029e8ea52e30", "FA9A8C87-A5C0-480C-88E2-1C48DC0D55B9", 100000, "merhcant test CC", "haha@haha.com", "ddddd ", "<<URL NOTIFY>>", 100000).generateHtml();
```



# Faspay Credit Void  Payment
```java
this example will generate the HTML of your browser via desktop platform, in android you can use WebView
# Faspay Credit Void  Payment
String html = new VoidRequestWrapperProd(new TestUserBaruCredit(), "e5f95232e08446cabda1b10ce6deb579", "042621B9-0FE3-4FDD-9350-97A4C931FF85", 10000, "ha", "haha@haha.com", "ddddd ", "<<URL NOTIFY>>").generateHtml();
```