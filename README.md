# suspicious-apk - quick analysis    

## We received a suspicious application to analyze
We are very happy that the companies are sharing their findings and doing their own reseach of APPs they use.

Today we have a Lithuanian software which is specifically designed to "Track and manage employee location" and being pushed to for various medical institutions (private sector and GOVs) via email.

![image](https://github.com/user-attachments/assets/41b59280-d402-494e-a73c-84c1ebffd3cc)    

![image](https://github.com/user-attachments/assets/5940f096-ee9e-4540-8105-4864f66f2573)
![are-you-sure-about-that-the-rock](https://github.com/user-attachments/assets/217ecb3e-029a-40fe-bd08-9baaac92133c)    

# There are few red flags within this APP    

1. APP can only be found on their website and not on the official page (understandable - it's just a startup)    

**But then everything goes downhill, I don't know where I should even start...**    

4. HTTP URLs in the source code. By default, the HTTP is insecure and fails to encrypt network traffic when necessary to protect sensitive communications.    
5. **Not only this Android application uses a hardcoded password in source code but also it's the default value:**     

**File Path:** "ch\qos\logback\core\net\ssl\SSL.java"

![Screenshot_8](https://github.com/user-attachments/assets/6d86a0d3-8d3a-420b-8c06-6ecbd0492834)    

6. **Stored API keys in source code:**    

![Screenshot_9](https://github.com/user-attachments/assets/c68b5d3d-dd6a-4e6a-b211-9225c8455dd8)    


7. **The android application used to generate random numbers in java is java.util.Random. Usage of java.util.Random class makes the random number generation cryptographically weak.**        
 
![image](https://github.com/user-attachments/assets/45652b53-7f19-4bd1-a793-caf002c45fd6)    

8. **Aplication uses the SHA-1 MessageDigest algorithm, which is weak.**    

![image](https://github.com/user-attachments/assets/dd94bf91-310b-4d18-b306-a1b4530f863e)    

And many more issues...

## The Privacy?    

![Screenshot_10](https://github.com/user-attachments/assets/3d0d0780-2c36-450d-81a5-c08283ef1e32) ![image](https://github.com/user-attachments/assets/fdf65bd8-b7f2-4895-9491-15276e567b5d)


**Examining Multiple Configuration Files**    
Telemetry could be sent to China & Russia it seems:    

![Screenshot_11](https://github.com/user-attachments/assets/8be3b0f1-dbb5-4b79-844e-a322b7fb48bd)    



The presence of separate JSON files (e.g., grs_sdk_global_route_config_extservice.json, grs_sdk_global_route_config_hianalytics.json, etc.) suggests the app uses different services or components, each with its own network settings. This is common in apps with diverse functionalities (analytics, location services, etc.).

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






## IOC    
- SHA256: c62d93af91062fd522166ccc1647e4b390e91b0b73f985e368da88b899d8f8e2    
- Android Package: com.atvykis
- Domain: hxxps://www.atvykis[.]lt
- App Version: 1.0
