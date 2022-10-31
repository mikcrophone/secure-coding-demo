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

Click Start for Apache and MYSQL Server

![XAMPP](https://user-images.githubusercontent.com/69864260/198924160-6e2506b7-34ea-42ae-9629-c3f9f18d1888.png)


Navigate to this address on your Chromium Browser

>localhost/ruko

Login using these credentials

>user: admin

>password: admin

![Ruko](https://user-images.githubusercontent.com/69864260/198924709-3192e859-8514-4b96-b00f-d5808b32a351.png)


## XSS Vulnerabilty

Navigate to Configurations -> Hoildays

![Holiday](https://user-images.githubusercontent.com/69864260/198926342-71172b4f-650e-4e0f-9413-2970d0d69cb3.png)




