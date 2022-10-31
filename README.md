# CVE-2022-43185 XSS Vulnerability Demo

Today I will be demonstrating a XSS Vulnerability in Rukovoditel 3.1.  Rukovoditel is a free web-based open source project management application.

This vulnerabity was found by Kubozz.

> https://nvd.nist.gov/vuln/detail/CVE-2022-43185

GitHub Documentation

> https://github.com/Kubozz/rukovoditel-3.2.1/issues/1

## Installation

Download Rukovoditel 3.1 Below with XAMPP. XAMPP is an open source web-server solution.  XAMPP launches the Ruko webserver.

> https://sourceforge.net/projects/rukovoditel/files/rukovoditel_3.1_xampp_php7.4.zip/download

**After downloading, be sure to extract the packages to your _C:_ Drive**

![ZIp](https://user-images.githubusercontent.com/69864260/198923901-a45d11af-2638-463c-9000-b98bdd681341.png)


## Launching Web Server

Navigate to your _C:_ Drive.

Locate and open the folder:
> xampp

Locate and open the application: 
> xampp-control

Click Start for Apache and MYSQL Server.

![XAMPP](https://user-images.githubusercontent.com/69864260/198924160-6e2506b7-34ea-42ae-9629-c3f9f18d1888.png)


Navigate to this address on your Chromium Browser.

>localhost/ruko

Login using these credentials.

>user: admin

>password: admin

![Ruko](https://user-images.githubusercontent.com/69864260/198924709-3192e859-8514-4b96-b00f-d5808b32a351.png)


## XSS Vulnerabilty

Navigate to Configurations -> Hoildays.

![Holiday](https://user-images.githubusercontent.com/69864260/198926342-71172b4f-650e-4e0f-9413-2970d0d69cb3.png)

Use **Burpsuite** to intercept browser.


Click **Add** and test out request.

![test](https://user-images.githubusercontent.com/69864260/198927382-b906e571-0db7-4108-9709-4bfdcc750c0c.png)

![test1](https://user-images.githubusercontent.com/69864260/198927393-c7a8bb51-a697-45e6-b4c5-9c6a49f6344b.png)

Send Request to the Repeater and test out Response.

![test3](https://user-images.githubusercontent.com/69864260/198928693-ad971009-72c7-4620-88c7-b06bcd8f0919.png)


Kubozz states that the vulnerability is in the name parameter.

They state that we can make use of the onerror event handler.

Here is a sample payload that we can use for the name parameter to return the current session cookie. **Remove the Space between the first quote and >**

> " ><img src=x onerror=alert(document.cookie);>

This payload will make the browser ouput "1" to the page.

> " ><img src=x onerror=alert(1);>


![test4](https://user-images.githubusercontent.com/69864260/198934108-87a37027-1e6c-4b06-9f1c-7d8acfc7c8e3.png)


![test5](https://user-images.githubusercontent.com/69864260/198934123-008f6217-7141-4675-a762-08ca2c2477cb.png)


An attacker with admin privleges could make use of this vulnerability.  These paylods are stored into the web servers database so everytime this page is loaded, these scripts will run one by one.

## Why?

Kubozz states that the _name_ parameter is vulnerable because the parameter does not encode any output that is reflected back to the page.  Removal of script tags is not enough.

### The Fix

First, stop the web server.

![XAMPP Stop](https://user-images.githubusercontent.com/69864260/198935230-99f286f8-8789-40b7-8a34-a82058b3a41f.png)


Go to your **C:** Drive and open _xampp_ in VS Code(Preferred)

Finding the actual source code for the vulnerable page was tricky because I cannot execute(or could not figure out how) the code to launch the webserver.  Nevertheless, I found the source code for the page.  

Go to this path.

> C:\xampp\htdocs\ruko\modules\holidays\actions\holidays.php


As we see in the source code, the web page uses PHP scripting language.

Go to line 18 of **holidays.php** and observe that the _name_ parameter does not use HTML Entity Encoded to encode any output to the webpage after submitted a holiday.

>             'name' => ($_POST['name']),

![vscode1](https://user-images.githubusercontent.com/69864260/198938623-51c3ae94-9aa8-486c-9d08-b43a53a0b96f.png)



I am not familiar with PHP scripting language but after doing research. I found out the proper way to encode the _name_ parameter.

> https://www.php.net/manual/en/function.htmlspecialchars.php


This how you would encode the _name_ parameter.  Replace line 18 with the following code.

>             'name' => htmlspecialchars($_POST['name']),

![VScode2](https://user-images.githubusercontent.com/69864260/198938709-9994e9ac-81ae-4145-9381-b2890f84a04f.png)


After replacing the code. Save the code.

Relaunch the web server using XAMPP.

Navigate yourself back to vulnerable page and you should notice that the previous payloads do not work because the _name_ parameter now encodes any output to the page.
















