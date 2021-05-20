# 80
![](../Attachments/Pasted%20image%2020210519164510.png)
### Nikto
```
---------------------------------------------------------------------------
+ Server: Microsoft-IIS/7.5
+ Retrieved x-powered-by header: ASP.NET
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Retrieved x-aspnet-version header: 2.0.50727
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Allowed HTTP Methods: OPTIONS, TRACE, GET, HEAD, POST 
+ Public HTTP Methods: OPTIONS, TRACE, GET, HEAD, POST 
+ 7863 requests: 0 error(s) and 7 item(s) reported on remote host
+ End Time:           2021-05-19 17:51:12 (GMT-4) (300 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```
### Gobuster Initial
```
===============================================================
2021/05/19 17:49:13 Starting gobuster in directory enumeration mode
===============================================================           
/UploadedFiles/       (Status: 403) [Size: 1233]            
/uploadedFiles/       (Status: 403) [Size: 1233]
/uploadedfiles/       (Status: 403) [Size: 1233]                                    
===============================================================
```
### Gobuster Extensions
```
===============================================================
2021/05/19 18:02:35 Starting gobuster in directory enumeration mode
===============================================================
/transfer.aspx        (Status: 200) [Size: 941]
/*checkout*.aspx      (Status: 400) [Size: 11] 
/*docroot*.aspx       (Status: 400) [Size: 11] 
/*.aspx               (Status: 400) [Size: 11] 
/http%3A%2F%2Fwww.aspx (Status: 400) [Size: 11]
/http%3A.aspx         (Status: 400) [Size: 11] 
/UploadedFiles/       (Status: 403) [Size: 1233]
/q%26a.aspx           (Status: 400) [Size: 11]  
/**http%3a.aspx       (Status: 400) [Size: 11]  
/*http%3A.aspx        (Status: 400) [Size: 11]  
/uploadedFiles/       (Status: 403) [Size: 1233]
/**http%3A.aspx       (Status: 400) [Size: 11]  
/http%3A%2F%2Fyoutube.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fblogs.aspx (Status: 400) [Size: 11]  
/http%3A%2F%2Fblog.aspx (Status: 400) [Size: 11]   
/uploadedfiles/       (Status: 403) [Size: 1233]   
/**http%3A%2F%2Fwww.aspx (Status: 400) [Size: 11]  
/s%26p.aspx           (Status: 400) [Size: 11]     
/%3FRID%3D2671.aspx   (Status: 400) [Size: 11]     
/devinmoore*.aspx     (Status: 400) [Size: 11]     
/children%2527s_tent.aspx (Status: 400) [Size: 11] 
/Wanted%2e%2e%2e.aspx (Status: 400) [Size: 11]     
/How_to%2e%2e%2e.aspx (Status: 400) [Size: 11]     
/200109*.aspx         (Status: 400) [Size: 11]     
/*sa_.aspx            (Status: 400) [Size: 11]     
/*dc_.aspx            (Status: 400) [Size: 11]     
/help%2523drupal.aspx (Status: 400) [Size: 11]     
/http%3A%2F%2Fcommunity.aspx (Status: 400) [Size: 11]
/Chamillionaire%20%26%20Paul%20Wall-%20Get%20Ya%20Mind%20Correct.aspx (Status: 400) [Size: 11]
/Clinton%20Sparks%20%26%20Diddy%20-%20Dont%20Call%20It%20A%20Comeback%28RuZtY%29.aspx (Status: 400) [Size: 11]
/DJ%20Haze%20%26%20The%20Game%20-%20New%20Blood%20Series%20Pt.aspx (Status: 400) [Size: 11]
/http%3A%2F%2Fradar.aspx (Status: 400) [Size: 11]                                                              
/q%26a2.aspx          (Status: 400) [Size: 11]                                                                 
/login%3f.aspx        (Status: 400) [Size: 11]                                                                 
/Shakira%20Oral%20Fixation%201%20%26%202.aspx (Status: 400) [Size: 11]                                        
/%22james%20kim%22.aspx (Status: 500) [Size: 3026]                                                             
/%22julie%20roehm%22.aspx (Status: 500) [Size: 3026]                                                           
/%22britney%20spears%22.aspx (Status: 500) [Size: 3026]                                                        
/http%3A%2F%2Fjeremiahgrossman.aspx (Status: 400) [Size: 11]                                                  
/http%3A%2F%2Fweblog.aspx (Status: 400) [Size: 11]                                                             
/http%3A%2F%2Fswik.aspx (Status: 400) [Size: 11]
```
---
## /transfers.aspx
![](../Attachments/Pasted%20image%2020210519184336.png)

