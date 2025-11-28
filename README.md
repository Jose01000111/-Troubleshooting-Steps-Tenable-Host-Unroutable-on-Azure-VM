# 🔍 Troubleshooting Steps — Tenable Host Unroutable on Azure VM

## I ran into a **“Host Unroutable”** error scanning my Azure Windows Server VM. The key fix was selecting the **Internal Scanner + Local scan engine-01**. 🔑  

## 1️⃣ **Verify the VM was actually running**  
## Azure showed the VM as *Stopped (deallocated)*. Tenable cannot route to a deallocated VM.  

<img width="659" height="386" alt="eax99oy" src="https://github.com/user-attachments/assets/c5d3ad33-69e7-4de0-9815-9e8c72574aee" />

> ### Action Taken:** Start the VM → wait for *“Running”*. ✅

## 2️⃣ **Confirm the correct scanner type (THIS FIXED THE ISSUE!)**  
## When scanning a private IP, the **main reason for Host Unroutable was using the wrong scanner**.  

<img width="534" height="129" alt="0UHM2cX" src="https://github.com/user-attachments/assets/67322187-fd7d-4166-ad7f-d85d7dd0dfca" />

> - Scanner Type: **Internal Scanner**  
> - Scanner: **Local scan engine-01**  

## 💡 Using the Tenable Cloud Scanner on a private IP automatically causes *“Host Unroutable”*.  
## **This was the key fix that finally allowed the scan to run.** 🎯

## 3️⃣ **Make sure both Tenable and the VM use the same VNet**  
## My VM is in:  *Cyber-Range-VNet / Cyber-Range-Subnet*  

<img width="334" height="47" alt="bnMfYvo" src="https://github.com/user-attachments/assets/13425e76-dd55-4e87-b8f2-41ee62bf5fea" />

> If the internal scanner is in a different VNet or the networks are not peered, Tenable cannot reach the target. 🌐

## 4️⃣ **Re-enter the private IP manually**  
## Copy/pasting the IP from Azure can add invisible characters.  

<img width="426" height="64" alt="svb0ZIq" src="https://github.com/user-attachments/assets/db71eb48-c106-4cfa-aa09-7464f8b36caa" />

> **Fix:** Type the IP manually → *10.0.0.131* ✏️

## 5️⃣ **Confirm the scan has actually started running**  
## After fixing routing + scanner selection:  

<img width="1113" height="28" alt="TIf67NN" src="https://github.com/user-attachments/assets/53bab95c-e8fe-4494-a21d-fc22bfcc1d99" />

> - Refresh the Tenable scan page 🔄  
> - Status should change from *Pending / Queued* → *Running* ✅  
> - If running → routing is fixed  
> - If still stuck → scanner cannot reach the host ❌
