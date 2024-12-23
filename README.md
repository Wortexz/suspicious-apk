# suspicious-apk - quick analysis    

## We received a suspicious application to analyze
We are very happy that the companies are sharing their findings and doing their own reseach of APPs they use.

**Big thanks to HILA.LT for sharing info about this app.**

Today we have a Lithuanian software which is specifically designed to "Track and manage employee location" and being pushed to for various medical institutions (private sector and GOVs) via email.

![IMG_20241223_164859](https://github.com/user-attachments/assets/d0b91661-2a83-4305-8c9d-bcc115594e15)  

## The website:  

![image](https://github.com/user-attachments/assets/41b59280-d402-494e-a73c-84c1ebffd3cc)    

![image](https://github.com/user-attachments/assets/5940f096-ee9e-4540-8105-4864f66f2573)
![are-you-sure-about-that-the-rock](https://github.com/user-attachments/assets/217ecb3e-029a-40fe-bd08-9baaac92133c)    

## There are few red flags within this APP    

1. APP can only be found on their website and not on the official page (understandable - it's just a startup)

**But then everything goes downhill, I don't know where I should even start...**    

2. HTTP URLs in the source code. By default, the HTTP is insecure and fails to encrypt network traffic when necessary to protect sensitive communications.    
3. **Not only this Android application uses a hardcoded password in source code but also it's the default value:**

**File Path:** "ch\qos\logback\core\net\ssl\SSL.java"

![397535899-c68b5d3d-dd6a-4e6a-b211-9225c8455dd8](https://github.com/user-attachments/assets/d50e3301-fb55-4057-9a6b-b28558f2ecac)  

4. **Stored API keys in source code:**    

![397535899-c68b5d3d-dd6a-4e6a-b211-9225c8455dd8](https://github.com/user-attachments/assets/f6c49889-89dc-4f31-89d4-12550d92739d)  


5. **The android application used to generate random numbers in java is java.util.Random. Usage of java.util.Random class makes the random number generation cryptographically weak.**        
 
![image](https://github.com/user-attachments/assets/45652b53-7f19-4bd1-a793-caf002c45fd6)    

6. **Aplication uses the SHA-1 MessageDigest algorithm, which is weak.**    

![image](https://github.com/user-attachments/assets/dd94bf91-310b-4d18-b306-a1b4530f863e)    

And many more issues...

## The Privacy?    

![Screenshot_10](https://github.com/user-attachments/assets/3d0d0780-2c36-450d-81a5-c08283ef1e32) ![image](https://github.com/user-attachments/assets/fdf65bd8-b7f2-4895-9491-15276e567b5d)


**Examining Multiple Configuration Files**    
Telemetry could be sent to China & Russia it seems:    

![Screenshot_11](https://github.com/user-attachments/assets/8be3b0f1-dbb5-4b79-844e-a322b7fb48bd)    



The presence of separate JSON files (e.g., grs_sdk_global_route_config_extservice.json, grs_sdk_global_route_config_hianalytics.json, etc.) suggests the app uses different services or components, each with its own network settings. 
This is common in apps with diverse functionalities (analytics, location services, etc.).  

**Presence of Chinese and Russian Domains:**    

Domains ending with .cn (China) and .ru (Russia) are present.
This could be a red flag, especially if the app is not targeting users in these regions, as it may suggest potential privacy concerns.

In the APK source code we can also find some certs:

![image](https://github.com/user-attachments/assets/7c69fdaf-8505-4747-8844-fe836f7bd879) ![image](https://github.com/user-attachments/assets/3dd66401-4385-4cb6-8afe-559cb98d3e7f)

More strange implementation methods:    

![image](https://github.com/user-attachments/assets/405c46c8-0dc2-49e5-829c-e72782e045ee)    

**And more:**  
AndroidManifest.xml file. The Android application exports a component to use other android applications but does not properly restrict which application can launch the feature or access the data it contains. If access to an exported Service is not restricted, any application would start and bind the service. It may allow a malicious application to perform unauthorised actions, increase access to sensitive information, or corrupt the application's internal state based on the exposed functionality.  

![Screenshot 2024-12-20 085002](https://github.com/user-attachments/assets/d60554d9-ecef-4b62-8da8-71eeb02f8b6d)  
![Screenshot 2024-12-20 085015](https://github.com/user-attachments/assets/6f8bbc5f-4368-425e-87a6-1548bdc2ce74)  

# Checking APP on VirusTotal
We can confirm that the APP is not malicious.  

![image](https://github.com/user-attachments/assets/7e9c71ca-6beb-4945-96c2-3ee331509e44)  

# Dynamic APP testing  
Downloaded suspicious APK file and installed it on our testing device.  


**When logging in we see that there is active communication to this server: "atvykis-be-3cc242149b04.herokuapp[.]com"**  
SSL certificate is valid until	Mon, 31 Mar 2025 23:59:59 UTC (expires in 3 months)  

![image](https://github.com/user-attachments/assets/cc3d50a7-ea9d-4519-8300-7b59423f7285)  


**Although this domain "herokuapp[.]com" seems to be clean in terms of malware - SSL certificate expired a year ago:**   

![image](https://github.com/user-attachments/assets/b9433b20-1db9-4757-b2f2-5f7aba03f247)  


Domain belongs to:  

![image](https://github.com/user-attachments/assets/c0d4f655-6d7e-40fd-9bca-5bfa2db9487f)  



## IOC    
- SHA256: c62d93af91062fd522166ccc1647e4b390e91b0b73f985e368da88b899d8f8e2    
- Android Package: com.atvykis
- Domain: hxxps://www.atvykis[.]lt
- App Version: 1.0
