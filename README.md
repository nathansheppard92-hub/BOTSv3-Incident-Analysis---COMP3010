# COMP 3010 Security Operations & Incident Management
## Coursework 2 – BOTSv3 Incident Analysis and Presentation
## Nathan Sheppard


# Table of Contents

<img width="621" height="234" alt="image" src="https://github.com/user-attachments/assets/e2bc04ba-0ba6-4558-90c2-14146a42b229" />


# Introduction

Showcase Video: https://www.youtube.com/watch?v=U8BXT928EbI

This report presents an investigation and analysis of the BOTSv3 dataset. This is a security dataset created by Splunk, which can be used to investigate a cyber-attack on a fictional company called Frothly.  

This report will document the relevance of SOC tiers and incident handling methodologies in the context of this scenario. SOCs are responsible for analysing and responding to threats to a company constantly ​[1]​, which will improve a company's threat intelligence and ability to respond to cyber-attacks quickly, to minimise damage. Identifying suspicious activity or potential misconfigurations in a network is crucial for SOC analysts, to protect a company and decrease the likelihood of cyber-attacks.  

The scope of this report will be focusing on the AWS related 200-level questions. It will show Splunk analysis of AWS CloudTrail and endpoint-related events, which will discover signs of suspicious activity within the network. Other parts of the incident such as network traffic email analysis are outside of the scope for this report.  

The aim of this is to investigate the incident to determine what occurred and identify company vulnerabilities. This knowledge can be used to improve overall SOC operations in the company, so they are able to detect threats much faster and easier and prevent future cyber-attacks.  

# SOC Roles & Incident Handling Reflection 

SOC roles are broken down into 3 tiers, with different responsibilities. 

A tier one SOC analyst would focus on basic threat analysis and real-time monitoring ​[2]​. They would handle common security incidents and gather information, including the severity of the threat and what resources it affects ​[3]​, to escalate more serious incidents to higher SOC tiers. Within the context of the BOTSv3 dataset, tier one SOC analysts would use SIEM tools such as Splunk to monitor AWS CloudTrail to look for suspicious API calls.  

A tier two SOC analyst would handle incidents escalated by tier one analysts and perform more in-depth assessments ​[4]​. They will assess the damage of an attack and how to respond to it. In this context, they would look further into suspicious API calls flagged by tier one analysts and assess if it is a real threat, and how they are going to respond.  

A tier three SOC analyst mainly focuses on threat hunting ​[2]​ and suggesting improvements for the company. This role is crucial for a company to consistently become more secure, as tier three analysts will look at the most advanced threats and find mitigation to prevent them repeating. In this context, they would search for causes of these incidents and misconfigurations, so that AWS can be made more secure in the future.  

 

The prevention phase is important to ensuring cyber-attacks are less frequent and cause minimal damage. This would mainly be dealt with by tier three SOC analysts, as they would locating vulnerabilities in the system. In this context and example could be misconfigurations in AWS, which would be fixed quickly to prevent events like account break-ins and permission misuse. This constant improvement shows the importance of SOCs, as the company will find vulnerabilities before hackers can and prevent many cyber-attacks.  

The detection phase consists of constant monitoring of systems to find signs of potential incidents. This would be conducted by SOC analysts in the BOTSv3 context by monitoring Splunk for suspicious AWS activity.  

The response phase is mostly done by tiers two and three analysts, as it is the immediate action taken against an attack. This shows the importance of a SOC, as a quick response is integral to minimise damage to the company systems.  

The recovery phase takes place after an attack, in this context reconfiguring affected AWS systems and ensuring they are secure once again. This would be used by tier three analysts to make recommendations for improvement, making the company more secure. 

# Installation & Data Preparation 

This section will document the installation of Splunk, and the preparation of the BOTSv3 dataset.  

Splunk is a very popular resource for SIEM in SOCs, as it provides many tools for investigations of cyber-attacks and monitoring of systems.  

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/d027dd41-e54a-44bc-bb7d-f68821027072" />

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/0775ee79-1b17-41c7-af6d-e07f33bbc422" />

The latest version of Splunk, 10.0.2 was downloaded. It is important to always use the latest version in a SOC, as this provides the most secure version with the latest features. Security is the most important aspect of this, as outdated software increase risk of vulnerabilities [5]. These could be exploited leading to cyberattacks. The wget command was ran in a terminal, installing Splunk onto the virtual machine.

<img width="939" height="525" alt="image" src="https://github.com/user-attachments/assets/d4379f61-478f-4a58-92cd-0b9baf54adeb" />

Once installed, Splunk was started using sudo ./splunk start, using sudo for administrator privileges. This reflects what would happen in an actual SOC, as higher privileges should be needed to use resources like SIEM due to them being dangerous to company security if used maliciously. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/d747032a-ad10-4c99-947f-3ba2638ed663" />

A Splunk account is created, using a secure password using a combination of letters, numbers and symbols. In the context of an SOC, Splunk can be a very powerful tool if accessed by users with malicious intent, so using a secure password is neccessary to prevent it being used inappropriately. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/4b993d5b-63ac-4d18-b769-42bed0ad84b5" />

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/d8d8d27f-ae5a-44c5-8148-9166bf3e0d1d" />

After Splunk was set up, the BOTSv3 dataset was also downloaded. Administrator privileges are also necessary for sudo commands in the terminal, as this is a very powerful tool that could be used maliciously if easily accessed. With this password, it ensures only authorised users can access resources such as Splunk. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/7e1d0b98-6e3f-46e8-a859-3a149ad1640a" />

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/e811200e-7703-4752-8f14-387c3e245344" />

Once downloaded, Splunk is started and loads the dataset. Data validation was completed to show the dataset was loaded correctly, by using the query:
index=botsv3 sourcetype=”aws:cloudtrail”
This proves that AWS CloudTrail logs in the correct dataset are present. Fields that are important to the investigation such as timestamps and event details, usernames, actions taken and IP addresses are all shown to be loaded properly, meaning the analysis can start. 

# Guided Questions

This report covers an incident that happened in the Frothly company, occurring on 8/20/2018 at 14:04:17. 

<img width="939" height="527" alt="image" src="https://github.com/user-attachments/assets/1ff3d363-fb3e-416d-9863-cb4aff2aca18" />

This Splunk command above was entered to locate the suspicious file upload. 

<img width="939" height="417" alt="image" src="https://github.com/user-attachments/assets/563a3e67-9f1c-4b25-87af-58e9df772d14" />

This log was found to be where the file was uploaded, showing the timestamp of this incident. How this was found will be shown later in the report. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/d37f4b64-1840-40bf-b68b-61677ed2aaa2" />

The investigation started with this command above being entered to find what IAM (Identity & Access Management) users accessed AWS in the company. This is a common first step for SOC investigations, as it will provide a list of potentially suspicious users. This provided a list of the users bstoll, btun, splunk_access and web_admin. It can be assumed that one of these users uploaded the file. This narrows down the investigation, and these names are seen as suspects by the tier one SOC analyst. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/a9e39db8-e17f-494f-a11a-51bc70a6f8d1" />

The above screenshot shows that AWS API activity was done without MFA. This could be suspicious as MFA is commonly used to properly authenticate a user and reduce the risk of an account being compromised. Without this, it is much more likely that this activity was done by a malicious unauthenticated user. This would be flagged immediately due to suspicion of malicious activity by tier one SOC analysts. Tier three SOC analyst's role here would be to report this as a security risk and recommendation to improve, so that the company is aware and can ensure MFA is always active. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/2ef63476-f232-453a-b9ae-96ab22e24e69" />

It was found that the processor number used on the web servers was E5-2676. This was checked for by tier one analysts as general information to be escalated to higher level analysts in serious events. Information like this can be used to check things like performance for suspicious activity on specific machines. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/4e2589b7-c2be-465d-95ed-ed3771c9e1fe" />

The command above was used to check S3 Bucket activity.

<img width="939" height="344" alt="image" src="https://github.com/user-attachments/assets/411e2412-0e62-4974-8f38-5da6351fe842" />

<img width="939" height="139" alt="image" src="https://github.com/user-attachments/assets/b3ff9466-8675-4c23-ac56-fa1cbcf1e02e" />

An S3 Bucket was found to be made publicly accessible at 14:01:46. This is a common misconfiguration in AWS which is a major security risk as it allows unauthorised users to upload or modify data. This would be flagged by the tier one analyst as highly suspicious due to the risk of having malicious data uploaded to the bucket. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/97364295-ba98-4d16-8f25-18a3b556e7ad" />

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/8a05b41e-1e11-48a1-b064-6d9c5fecfe98" />

The CloudTrail event showing the bucket being made public was found, with the event ID ab45689d-69cd-41e7-8705-5350402cf7ac. The username tied to this action was the IAM user bstoll, a name found previously at the start of the investigation. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/0088c764-a37b-4519-a8ce-66b6010bcd5b" />

<img width="939" height="167" alt="image" src="https://github.com/user-attachments/assets/fc5c4f1c-eafc-42d5-b836-bd3fc3336459" />

This user also set the buckets permissions back to private at 14:57:54. This would be flagged for investigation by higher analysts of the user by the tier one analyst, as this sequence of events implies the modifications were purposeful, likely with malicious intent. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/e9bf0612-e5b7-424d-883b-6f9deb318b7b" />

The name of this bucket was found to be frothlywebcode. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/82642439-30fb-4ede-8957-9bb84dabd8d5" />

This command was entered to find the name of the text file uploaded while the bucket was public. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/cec7a1ff-1b98-41bb-a6dc-da92b9e2be09" />

The file was found to be named OPEN_BUCKET_PLEASE_FIX.txt.

<img width="939" height="417" alt="image" src="https://github.com/user-attachments/assets/7f88fc4d-ff02-49db-861c-e5ab1bdf8103" />

Another file was found to be uploaded while the bucket was public, being a tar.gz file, also by bstoll. Tar files are used to create a single file from many files [6] and is an easy and quick way for users to upload malicious files. This in combination with the purposeful modification of bucket access would be incredibly suspicious to the tier one analyst, so flagged for investigation immediately. This is a security risk as it shows a malicious user is accessing the system, potentially uploading harmful files. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/a7b383d3-67fa-40fa-ac12-7dfd5755f561" />

<img width="939" height="394" alt="image" src="https://github.com/user-attachments/assets/9226fe5c-b57f-4384-aa83-597341d86556" />

This command being entered also shows the user bstoll accessing coinhive.com 21 times while the bucket was public. This is a crypto mining website, which would immediately be escalated by the SOC analyst to higher tiers. This is due to the user performing unauthorised mining on a company system, affecting performance and being a security risk. Unauthorised software could be dangerous for the company and can lead to malware installations.  It is also possible the system is being cryptojacked, a method of hijacking a machine for crypto mining [7]. 

<img width="939" height="528" alt="image" src="https://github.com/user-attachments/assets/a9661a05-b75b-4b63-bb10-70d1d24d2a74" />

It was found that an endpoint with the FQDN BSTOLL-L.froth.ly was running a different operating system than the others, which would be flagged suspicious and for investigation. This is due to the inconsistency compared to all other systems, which would indicate bstoll is using a machine with elevated permissions, a major security risk. 
After this investigation by the tier one analyst this user would be investigated by higher tiered analysts, due to high suspicion of uploading malicious content to the bucket while public, and crypto mining on company systems, potentially due to the account being compromised. 

# Conclusion

To summarise, an S3 bucket was made public by IAM user bstoll, which allowed potentially malicious files to be uploaded. Further investigation also revealed the account was using a Windows Enterprise OS machine likely with heightened access to vist coinhive.com, a popular crypto mining site. This is a major security issue that puts the company Frothly at risk. 
A lack of MFA was discovered to be the cause of this, as AWS CloudTrail was accessed without the use of MFA, suggesting the account may have been compromised. This is something that would be flagged in a SOC environment by tier three analysts as something to improve upon. Including MFA would decrease the risk of accounts being compromised by 99% [8], ensuring the company is much safer. 
General monitoring is also something to improve on, as the malicious user was able to act for around an hour before setting the bucket back to private. Resources like alerts and better use of Splunk would allow Frothly to discover suspicious activity much earlier and prevent hackers from dealing as much damage. 
Without these improvements the company is at serious risk of another cyber-attack. 
Investigations like this also reflect the usefulness of SOC strategies in the company. With this investigation, vulnerabilities like MFA were discovered. Tier one analysts found this and the suspicious activity, and important risks and information were reported to higher level analysts if further investigation was required. 
Overall, SOC analysis proves to find vulnerabilities that the company needs to resolve, while also allowing tier one analysts to perform general monitoring to discover potential threats to the company. This system is very effective and will keep the company secure and improves early threat detection and incident response.

# References

[1] 	B. Buckman, “What is a SOC? Why Every Company Needs One (Yesterday),” Huntress, 12 August 2025. [Online]. Available: https://www.huntress.com/soc-guide/what-is-soc?hnt=7owbagafxvsq. [Accessed 26 December 2025].

[2] 	I. Assaf, “SOC Analyst Tier 1 vs. Tier 2 vs. Tier 3: Key Differences & Responsibilities,” Radiant, 17 January 2025. [Online]. Available: https://radiantsecurity.ai/learn/soc-tier-1-vs-tier-2-vs-tier-3/. [Accessed 26 December 2025].

[3] 	W. E. Team, “Tier 1 SOC analysts : Responsibilities and career path,” Wiz, 6 November 2025. [Online]. Available: https://www.wiz.io/academy/cloud-careers/soc-analyst-tier-1. [Accessed 27 December 2025].

[4] 	paloalto, “Security Operations Center (SOC) Roles and Responsibilities,” paloalto, n.d.. [Online]. Available: https://www.paloaltonetworks.co.uk/cyberpedia/soc-roles-and-responsibilities. [Accessed 27 December 2025].

[5] 	N. C. S. Centre, “Device security guidance,” National Cyber Security Centre, n.d.. [Online]. Available: https://www.ncsc.gov.uk/collection/device-security-guidance/managing-deployed-devices/obsolete-products. [Accessed 28 December 2025].

[6] 	NullByte, “Linux Basics for the Aspiring Hacker: Archiving & Compressing Files,” NullByte, 13 November 2015. [Online]. Available: https://null-byte.wonderhowto.com/how-to/linux-basics-for-aspiring-hacker-archiving-compressing-files-0166153/. [Accessed 28 December 2025].

[7] 	NHS, “Coinhive and Cryptojacking,” NHS, 12 October 2017. [Online]. Available: https://digital.nhs.uk/cyber-alerts/2017/cc-1699. [Accessed 30 December 2025].

[8] 	L. A. Meyer, “How effective is multifactor authentication at deterring cyberattacks?,” Microsoft, n.d. May 2023. [Online]. Available: https://www.microsoft.com/en-us/research/publication/how-effective-is-multifactor-authentication-at-deterring-cyberattacks/. [Accessed 30 December 2025].

# Generative AI Declaration

<img width="689" height="533" alt="image" src="https://github.com/user-attachments/assets/678be464-9a82-479d-bf56-67b59a0361da" />

