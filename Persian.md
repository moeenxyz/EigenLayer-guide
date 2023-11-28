
<h1 align="center"> راهنمای عملیاتی Node EigenLayer </h1>

## 👽 این آموزش گام به گام به شما در راه اندازی و اجرای یک گره در EigenLayer کمک خواهد کرد.

### لینک‌های من
 * [توییتر ](https://twitter.com/Moeenxyz)
* [لنز ](https://lenster.xyz/u/moeen)

اگر این راهنما مفید بود، در نظر داشته باشید به من دلیگیت کنید:
* [Node](https://goerli.eigenlayer.xyz/operator/0xe3c694453d69caea4edcbb0bb8d24accc6932565)

## راه اندازی نود

انتخاب یک VPS

یک VPS انتخاب کنید. برای Operatorها حداقل تنظیمات مشخص نشده، اما اگر می‌خواهید AVS ران کنید، به موارد زیر نیاز دارید:
تعداد vCPUs: 16
حافظه: 32 گیگابایت
فضای ذخیره‌سازی: 3.6 ترابایت (حجم SSD با عملکرد بالا)
معادل EC2: m5.4xlarge
استفاده مورد انتظار از شبکه:
مصرف پهنای باند کلی دانلود: 24 مگابیت بر ثانیه
مصرف پهنای باند آپلود: 120 مگابیت بر ثانیه
حداکثر پهنای باند شبکه (آپلود/دریافت): 1 گیگابیت بر ثانیه

من شخصا از Hetzner استفاده می‌کنم. این لینک به شما  20 یورو اعتبار می‌ده:

 * [Hetzner](https://hetzner.cloud/?ref=p7amgYr2ILM7)

نیازمندی‌های سیستم عامل

.سیستم عامل: Ubuntu 22.04
.پردازنده پیشنهادی: AMD

## بروزرسانی سیستم عامل لینوکس شما

```shell
sudo apt update
```

```shell
sudo apt upgrade
```


## 👽 نصب Docker و Docker Compose

```shell
# کلید رسمی Docker رو اضافه کنید:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# مخزن رو به منابع Apt اضافه کنید:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

سپس اجرا کنید:

```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

برای تست، پس از اجرای دستور زیر، اگر پیام تایید نشان داده شد، همه چیز محیاست.

```shell
sudo docker run hello-world
```

نصب Docker Compose

```shell
$ sudo apt install docker-compose
```

```shell
sudo curl -L https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

```shell
$ sudo chmod +x /usr/local/bin/docker-compose
```

```shell
$ docker compose version
```

پس از اجرا باید پیام زیر رو ببینید:
Docker Compose version vX.XX.X

حالا وقت نصب eigenlayer CLI است،

در حال حال حاضر، آخرین نسخه 0.4.3 است، می‌توانید نسخه رو با بررسی مخزن GitHub تیم به روز کنید.

 برای Linux/amd64 :

```shell
curl -L https://github.com/NethermindEth/eigenlayer/releases/download/v0.4.3/eigenlayer-linux-amd64 --output eigenlayer
chmod +x ./eigenlayer
```

سپس:

```shell
chmod +x ./eigenlayer
```

حالا شما eigenlayer رو نصب کردید.

 کلیدها را ایجاد کنید و لیست کنید. 
کلمه کلیدی [keyname] رو به نام دلخواه خودتون تغییر بدید.

```shell
./eigenlayer operator keys create --key-type ecdsa [keyname]
./eigenlayer operator keys create --key-type bls [keyname]
```

در این مرحله برنامه از شما درخواست رمز عبور برای رمزگذاری کلید خصوصی ECDSA و BLS می‌شه. دو مرحله داره و می‌تونید از دو رمز مجزا یا شبیه هم استفاده کنید، رمز رو در جای دیگه‌ای ایجاد کنید و اینجا پیست کنید. 

خروجی شامل 
ECDSA Private Key (Hex), Key location, Public Key hex, Operator Ethereum Address, BLS Private Key, BLS Public Key
هست که باید اون‌ها رو ذخیره کنید و کلیدهای خصوصی رو در جایی امن ذخیره کنید.

اگر می‌خواهید کلید خودتون رو وارد کنید، مستندات EigenLayer رو بررسی کنید.
https://docs.eigenlayer.xyz/operator-guides/operator-installation#import-keys

الان باید نود خودتون رو ثبت‌نام کنید.

ابتدا این اطلاعات رو تکمیل کنید، فایل رو به نام metadata.json ذخیره کنید و در جایی عمومی آپلود کنید. مطمئن شوید که لوگو با فرمت .png باشه و عمومی باشه لینکش. لینک به این فایل متادیتا رو ذخیره کنید.

```json
{
  "name": "اسم نود شما",
  "website": "https://www.example.com",
  "description": "توضیحات",
  "logo": "https://www.example.com/logo.png",
  "twitter": "https://x.com/example"
}
```

سپس اجرا کنید:

```shell
./eigenlayer operator config create
```

و تمام اطلاعاتی که می‌خواد رو تکمیل کنید، مانند زیر:

```shell
Would you like to populate the operator config file? Yes
Enter your operator address: [your operator address from previous steps]
Do you want to gate stakers approval? No
Enter your earnings address (default to your operator address): [your wallet address for earnings]
Enter your ETH rpc url: [e.g., https://rpc.ankr.com/eth_goerli]
Enter your ecdsa key path: [your ecdsa Key location]
Enter your bls key path: [your bls Key location]
Select your network: goerli
```
سپس اجرا کنید:

```shell
nano operator.yaml
```

و این اطلاعات رو اضافه کنید:
از این لینک برای دریافت آدرس به روز شده قرارداد هوشمند استفاده کنید
[https://docs.eigenlayer.xyz/operator-guides/operator-installation#goerli-smart-contract-addresses]

```yaml
metadata_url: لینک به metadata.json شما
el_slasher_address: 0xD11d60b669Ecf7bE10329726043B3ac07B380C22
bls_public_key_compendium_address: 0xc81d3963087Fe09316cd1E032457989C7aC91b19
```

حالا مقداری GoerliETH به آدرس Operator خودتون که در مرحله قبل به دست آوردید، انتقال بدید،
سپس اجرا کنید:

```
./eigenlayer operator register operator-config.yaml
```

بعد از انجام این کار، بررسی کنید که همه چیز درست انجام شده:

```
./eigenlayer operator status operator.yaml
```

اگر پیام زیر را دیدید همه چیز درست هست،
Operator is registered

حالا به این آدرس بروید:
[https://goerli.eigenlayer.xyz/operator/]
و نود خودتون رو بررسی کنید.

اگر این مطلب را دوست داشتید، در نظر داشته باشید که به من دلگیت کنید و این مطلب را ستاره دار کنید.:
[https://goerli.eigenlayer.xyz/operator/0xe3c694453d69caea4edcbb0bb8d24accc6932565]
```
