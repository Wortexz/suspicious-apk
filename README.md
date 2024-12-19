# suspicious-apk - quick analysis    

## We received a suspicous applcation to analyze
We are very happy that the companies are sharing their findings and doing their own reseach of APPs they use.

Today we have a Lithuanian software which is specifically designed to - "Track and manage employee location" and being pushed to for various medical institutions (private sector and GOV).

![image](https://github.com/user-attachments/assets/41b59280-d402-494e-a73c-84c1ebffd3cc)    

![image](https://github.com/user-attachments/assets/5940f096-ee9e-4540-8105-4864f66f2573)
![are-you-sure-about-that-the-rock](https://github.com/user-attachments/assets/217ecb3e-029a-40fe-bd08-9baaac92133c)    

# There are few red flags within this APP    

1. APP can only be found on their website and not on official page (understandable - it's just a startup)
**But then everything goes downhill, don't know where should I even start...**
2. HTTP URLs in the source code. By default, the HTTP is insecure and fails to encrypt network traffic when necessary to protect sensitive communications.
3. Not only this Android application uses a hardcoded password in source code but also it's the default value:        

![Screenshot_8](https://github.com/user-attachments/assets/6d86a0d3-8d3a-420b-8c06-6ecbd0492834)    

5.  




## IOC    
- SHA256: c62d93af91062fd522166ccc1647e4b390e91b0b73f985e368da88b899d8f8e2    
- Android Package: com.atvykis    
