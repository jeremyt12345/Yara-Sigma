# Yara-Sigma
Yara &amp; Sigma-HTB Notes 14/15


"YARA and Sigma are two essential tools used by SOC analysts to enhance their threat detection and incident response capabilities. They empower analysts with improved threat detection capabilities, efficient log analysis, malware detection and classification, IOC identification, collaboration, customization, and integration with existing security tools."

Yara is signature based detection that is open source way to detect malware in your enviroment.


Watching this video to get an overreview

<img width="1087" height="709" alt="image" src="https://github.com/user-attachments/assets/afb30f70-b477-4c84-b89f-63b0277be96c" />


Usages of Yara

<img width="952" height="798" alt="image" src="https://github.com/user-attachments/assets/5beda283-03c3-4889-b70b-766e691f5a59" />



YARA Rule Breakdown:

1. Rule Header
2. Rule Meta
3. Rule Body
4. Rule Conditions


Before I go into the questions I am to first to understand the process behind crafting a YARA rule by following this HTB prompt

-I ssh'd into the ip then ran the prompts:

cd /home/htb-student/Samples/YARASigma
ls
strings svchost.exe

"From the first few strings, it becomes evident that the file is packed using the UPX (Ultimate Packer for eXecutables) packer. Given this discovery, we can incorporate UPX-related strings to formulate a basic YARA rule targeting samples packed via UPX."

<img width="686" height="348" alt="image" src="https://github.com/user-attachments/assets/d19f9c1a-8af1-43e4-b08c-fad59fbd4bfc" />
