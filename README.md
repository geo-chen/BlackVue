# BlackVue

**Product**: Dashcam

**Version**: 590X


## Finding 1 - CVE-2025-30130: Unauthenticated Upload Endpoint on HTTP 

**Description**: Following CVE-2023-27746 (weak credentials) and CVE-2023-27747 (unauthenticated web server), an attacker can upload malicious code or even malware via the following endpoint: http://10.99.77.1/upload.cgi

![image](https://github.com/user-attachments/assets/a0111910-f0d8-4774-beb5-1c52767b836f)

**Vulnerability Type**: Incorrect Access Control

**Vendor of Product**: BlackVue

**Affected Product Code Base**: BlackVue Dashcam 590X

**Affected Component**: Upload mechanism

**Attack Type**: Remote

**Impact Code execution**: True

**Impact Information Disclosure**: True

**Attack Vectors**: A remote attacker can upload malware onto the dashcam via an unauthenticated upload endpoint on the dashcam's http server.

**Has vendor confirmed or acknowledged the vulnerability?**: Yes


## Finding 2 - CVE-2025-30128: Unauthenticated Modifications to Dashcam Configurations

**Description**: An attacker connected to the dashcam's network can perform more damage by draining and sabotaging the battery of the car.

Here's an example - this is an as-is config accessible over unauthenticated web server:

![image](https://github.com/user-attachments/assets/d51ec69b-9acd-4cb1-91ca-2bcadf9933b6)

Using the upload endpoint at http://10.99.77.1/upload.cgi, an attacker can add in misconfiguration to sabotage the car battery remotely:

![image](https://github.com/user-attachments/assets/ab3bb1bc-3a70-4c39-b34b-264ece664eb5)

**Vulnerability Type**: Incorrect Access Control

**Vendor of Product**: BlackVue

**Affected Product Code Base**: BlackVue Dashcam 590X

**Affected Component**: Unauthenticated Configuration Management

**Attack Type**: Remote

**Impact Code execution**: True

**Impact Information Disclosure**: True

**Attack Vectors**: A remote attacker can leverage on the lack of authentication on configuration management to disable battery protection on the dashcam to drain the car's battery.

**Has vendor confirmed or acknowledged the vulnerability?**: Yes

## Finding 3 - CVE-2025-2355: Hardcoded secrets exposed in plaintext + client secrets sent via GET

In the BlackVue v3.65 APK, both BCS_TOKEN and SECRET_KEY, along with the API endpoints, are exposed in the clear.
![image](https://github.com/user-attachments/assets/e2f09ff7-884f-42c7-9667-566ab8e7760e)

![image](https://github.com/user-attachments/assets/ab998eaf-1eaf-4f09-94ca-43de049506b7)

the bcsSignature is easily computed: 

![image](https://github.com/user-attachments/assets/27594907-cfed-4718-90e6-b2e6b860b9bf)


## Finding 4 - CVE-2025-2356: Unauthorised API calls to change settings such as delete device:

While most of the sensitive API endpoints require userToken, that is transmitted via GET parameter:
![image](https://github.com/user-attachments/assets/ea75d84d-e5eb-43bb-9c8b-b78111a3a67b)

Redacted image of a malicious call:

![image](https://github.com/user-attachments/assets/a4ed058e-b516-47e5-93d0-63286f4e31ef)


Why is this insecure? Because GET parameters are captured in browser history, referral URLs, or any proxy solutions. For instance, in a corporate environment, all endpoint URLs are captured, so if an employee uses the blackvue app, the usertoken, which is sensitive, would be logged by the proxy solution. With the user email + token and the hardcoded secrets, an attacker can make arbitrary changes or remotely control the account/device.

## Finding 5: Misconfigured Cloud Devices Exposing Live Feeds, Location, Even Car Plates
<in discussion>


## Disclosure Timeline

25 Feb 2025 - disclosed to BlackVue

26 Feb 2025 - acknowledged by BlackVue

5 Mar 2025 - accepted by BlackVue

16 Mar 2025 - CVEs published







