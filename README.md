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


---------------------------------------------------------------------------------------------------------------------------------
<img width="1110" height="268" alt="image" src="https://github.com/user-attachments/assets/92beafc3-7740-4178-87ad-71623625dcb4" />



---------------------------------------------------------------------------------------------------------------------------------
<img width="1912" height="914" alt="image" src="https://github.com/user-attachments/assets/7b16608f-b135-492f-abf5-db83a03b37f0" />


"Now, for the moment of truth. We'll unleash YARA with our newly minted rule to see if it sniffs out any matches when run against a malware sample repository located at home/htb-student/Samples/YARASigma inside this section's target."

<img width="1243" height="162" alt="image" src="https://github.com/user-attachments/assets/0fba57f4-55ad-41e2-bf91-186fa3edc8f7" />

-------------------------------------------------------------------------------------------------------------------------------------

Day 2

Manually Developing a YARA Rule

The rest of the article was going over examples of creating Yara Rules based on real attacks that happened and were documented such as this one: https://web.archive.org/web/20250607083048/https://www.ncsc.gov.uk/static-assets/documents/Turla%20group%20using%20Neuron%20and%20Nautilus%20tools%20alongside%20Snake%20malware_1.pdf


My goal was to solve this question and I did use AI but my plan is to use it minimally going forward.

Step 1: ssh into machine

ssh htb-student@IP 
Password:_______


<img width="1908" height="831" alt="image" src="https://github.com/user-attachments/assets/770b4522-f35f-457e-8f6d-e3b1361cb5f6" />



Day 3

My goal while doing these labs is not so much to get the cert (CDSA) but to understand each question to further my knowledge.

Q1: "Perform string analysis on the "DirectX.dll" sample that resides in the "/home/htb-student/Samples/YARASigma" directory of this section's target. Then, study the "apt_apt17_mal_sep17_1.yar" YARA rule that resides in the "/home/htb-student/Rules/yara" directory and replace "X.dll" with the correct DLL name to ensure the rule will identify "DirectX.dll". Enter the correct DLL name as your answer. Answer format: _.dll"

What is string analysis? 
- String analysis is a cornerstone of malware investigation, revealing embedded commands, URLs, and other artifacts that can expose a threat’s intent.

Now to find the rule we use the command 
"cat /home/htb-student/Rules/yara/apt_apt17_mal_sep17_1.yar"

<img width="879" height="326" alt="image" src="https://github.com/user-attachments/assets/495c0434-dc0c-402f-be07-11c3e0c903f0" />


Using process of elimination we can find the correct one.


From the command I found the placeholder. For reference I'm doing all this to replace the correct DLL so the rule can actually be detected.



<img width="883" height="486" alt="image" src="https://github.com/user-attachments/assets/09279b7b-98fe-4601-bd6f-bcafb315fb41" />


Now we want to see, match and confirm

Using this command check to see if there is a match in the rule, if we get a return we have a match

"yara /home/htb-student/Rules/yara/apt_apt17_mal_sep17_1.yar /home/htb-student/Samples/YARASigma/DirectX.dll"

<img width="877" height="309" alt="image" src="https://github.com/user-attachments/assets/60a24c2d-0f7e-4d97-9586-1cbca57b1520" />


....and no return


So now Im going into the file to edit the dll so we can get our rule match


<img width="983" height="536" alt="image" src="https://github.com/user-attachments/assets/a24307fe-5901-429a-a711-501a569983a2" />



The final test after this command we can confirm we got our match

"yara ~/apt17_fixed.yar /home/htb-student/Samples/YARASigma/DirectX.dll"

<img width="775" height="335" alt="image" src="https://github.com/user-attachments/assets/c1f3f940-fd65-433e-afab-cec8fbe4ca08" />
-----------------------------------------------------------------------------------------------------------------------------------------

Today I wanted to get a better understanding of Malware analysis and how and why I would be using Yara Rules. It previously didnt make sense to me why I would anazlyze malware on a machine on the network while its active. And Would I do that before or after an inicident? Here is what Claud AI explained??

"In real life the malware is already there because the detection rules come after something got through. The lab drops you into the middle of that story: the infection has happened, someone collected the sample, and now you’re the analyst.

Why the sample is “already on the device”

That HTB box (ACADEMY-YARASIGMA-FLARE) is a malware analysis workstation built on FLARE VM, Mandiant’s Windows analysis distro. It isn’t a victim machine, and nobody there got infected. The sample was put there on purpose so you could study it safely.

A real-world equivalent at EMS might go like this:

Something gets past your defenses. A phishing attachment slips through, Huntress flags a weird process, Darktrace sees odd beaconing, or a user reports their PC acting strange.
You collect the sample. You pull the file from quarantine, from the email, or from the endpoint, and grab a memory dump if it’s running.
You analyze it in an isolated VM. Like this HTB box, it’s a disposable machine off your real network. You run the sample and watch what it does: the strings it reveals, the files it drops, the connections it makes.
You write detections from what you learned:
A YARA rule for the file and memory traits unique to this malware.
A Sigma rule for the behavior it leaves in logs.
You hunt across the environment. The real question is never “is this one PC infected?” because you already know it is. The question is: did it land anywhere else that AV missed, and will we catch it next time?

So the malware being present isn’t the point. It’s the evidence you mine to build detections that protect every other machine."

Hunting Evil with YARA (Windows Edition)






