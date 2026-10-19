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


"Let's continue our dive into the world of YARA rules using a sample named dharma_sample.exe residing in the /home/htb-student/Samples/YARASigma directory of this section's target."

<img width="1910" height="601" alt="image" src="https://github.com/user-attachments/assets/b380456d-f363-4c41-a253-029ac5c27fac" />


"After we execute the strings command on dharma_sample.exe, we spot C:\crysis\Release\PDB\payload.pdb, which is pretty unique. Alongside other distinct strings, we can craft a more refined YARA rule. Let's employ yarGen to expedite this process."

<img width="1335" height="237" alt="image" src="https://github.com/user-attachments/assets/5b6158c9-bc1c-4897-b190-7c3fc4094297" />


Next Im told to run yarGen

"yarGen is our go-to tool when we need an automatic YARA rule generator. What makes it a gem is its ability to churn out YARA rules based on strings found in malicious files while sidestepping strings common in benign software. This is possible because yarGen comes equipped with a vast database of goodware strings and opcodes. Before diving in, we need to unpack the ZIP archives containing these databases."

<img width="915" height="155" alt="image" src="https://github.com/user-attachments/assets/960d9a9d-40af-4960-b6c5-3f590ab34623" />

<img width="1110" height="268" alt="image" src="https://github.com/user-attachments/assets/92beafc3-7740-4178-87ad-71623625dcb4" />


<img width="1912" height="914" alt="image" src="https://github.com/user-attachments/assets/7b16608f-b135-492f-abf5-db83a03b37f0" />


