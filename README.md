**Platform:** LetsDefend

**Module:** SOC140 - Phishing Mail Detected - Suspicious task Scheduler

**Difficulty:** Easy

**Target:** mark@letsdefend.io 

**Date:** 2026-06-13

---

<h3 align =center> Walkthrough </h3>

***Alert Review:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The very first thing you want to do is expand the alert and read every single field before jumping into the investigation.
<br>
<br>

<img width="1261" height="474" alt="p-1" src="https://github.com/user-attachments/assets/320ffc0e-3f15-4bee-a7c3-a09e4d9faf08" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; This alert is EventID 82, triggered on March 21, 2021 at 12:26 PM, under the rule SOC140 - Phishing Mail Detected - Suspicious Task Scheduler. That Device Action field is the first important thing to note here. Unlike a proxy alert where Allowed means the connection went through, here the email was Blocked — meaning it never reached the recipient.
<br>
<br>

---
***Starting the Playbook:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The first playbook step is parse Email, which is sking you to gather all the key information about the incoming email before doing any analysis.
<br>
<br>
</b>

<img width="598" height="336" alt="p-2" src="https://github.com/user-attachments/assets/b249ae2a-674b-480e-a979-66708443e191" />

<br>
<br>

- When was it sent? -> Mar 21, 2021, 12:26 PM

- What is the email's SMTP address? -> 189.162.189.159

- what is the sender address? -> aaronluo@cmail.carleton.ca

- what is the recipient address? -> mark@letsdefend.io

- Is the mail content suspicious? -> yes

- Are there any attachment? -> yes

&nbsp;&nbsp;&nbsp;&nbsp; You should never skip straight to analysis without first fully understanding what you're looking at.
<br>

---
***Examining the Email:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The playbook asks whether the email contains attachments or URLs.
<br>
<br>

<img width="606" height="335" alt="p-3" src="https://github.com/user-attachments/assets/e10aac0b-0236-4bba-b794-c98afcac169b" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; So, let's head over to Email Security and pull up the email.
<br>
<br>

<img width="1280" height="649" alt="p-4" src="https://github.com/user-attachments/assets/0fb14e50-3279-4b39-971d-62566ff2a364" />

<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; There is also an attachment with the hash 72c812cf21909a48eb9cceb9e04b865d. The attachment is password-protected with the password "infected" written right there in the email body itself. The answer is clearly Yes.
<br>
<br>

---
***Attachment Analysis:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; The playbook directs you to analyze the URL or attachment using third-party tools.
<br>
<br>

<img width="593" height="384" alt="p-5" src="https://github.com/user-attachments/assets/b3a20041-df68-487b-81c2-da174f6a1035" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; To get the attachment URL for analysis, simply right-click the attachment and copy the link address. This gives you the full download URL without actually downloading or executing the file. You never want to click or open a suspicious attachment directly on your own machine.
<br>
<br>

<img width="1280" height="597" alt="p-6" src="https://github.com/user-attachments/assets/44fda50b-98e3-43c1-986a-57276cf2d967" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; Here we submit the download URL associated with the attachment to VirusTotal.
<br>
<br>

<img width="1280" height="648" alt="p-7" src="https://github.com/user-attachments/assets/93fe0934-4bf4-4693-ae95-0e61a067a99a" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; The results come back with 14 out of 92 vendors flagging it as malicious. This is more than enough to confirm the attachment is malicious.
<br>
<br>

---
***Check if Mail was Delivered:***

<img width="598" height="279" alt="p-8" src="https://github.com/user-attachments/assets/1d7606ec-c99b-40f6-96b8-bb57b388cc28" />


<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; We already know the answer from the very first step, the Device Action was Blacked. That means the email security system caught it and the email never landed in mark's inbox.
<br>
<br>

---
***Document:***

<br>
&nbsp;&nbsp;&nbsp;&nbsp; You want to document everything you found that could help detect related activity in the future.
<br>
<br>

<img width="598" height="382" alt="p-9" src="https://github.com/user-attachments/assets/b4d1a6c9-5430-4733-bccb-be5556041b97" />

<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; Add the Phishing URL and Attacker SMTP IP for future reference.
<br>
<br>

<img width="595" height="372" alt="p-10" src="https://github.com/user-attachments/assets/cc987570-74fb-46e9-ba07-3d84109d8a8c" />

<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; Write your analyst note to tell the full story clearly.
<br>

---

<h3 align =center> Summary </h3>

<br>
&nbsp;&nbsp;&nbsp;&nbsp; Thiis was a confirmed True Positive phishing attempt that was successfully stopped by the security system. An email titled 'COVID19 Vaccine' was flagged as a phishing attempt and blocked by our security system. The email came from SMTP IP 189.162.189.159 and contained a malicious link. Because the system successfully blocked the email, it never reached the user, and no further action is needed. This case is closed as a True Positive
