# Build and Verify a Secure Two-Tier Web Application in Azure

### Objective

This SOP explains how to set up a secure two-tier web application with a public web tier and a private database tier. It also covers how to verify that only the web server can communicate with the database server.

### Link to Loom

<https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64>
### Key Steps

 

**1. Create the virtual network for the lab** 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d19f15d6-b931-4206-8ba4-e73416b6992d" />

- Open **Virtual Networks** in the Azure portal.
- Create or select the lab virtual network (example shown: **VNetLab2**).
- Confirm the network is ready before creating subnets and virtual machines.

 

**2. Create separate subnets for the web and database tiers** [0:16](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=16)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a1074e33-dc55-42ab-8a0e-b7b37255908f" />


- Create two subnets inside the virtual network: 
  - **web** subnet
  - **db** subnet
- Place the web server in the web subnet.
- Place the database server in the db subnet.
- Ensure the db subnet is configured for private access only.

 

**3. Restrict the database tier to private access** [0:22](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=22)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/931b031b-dc5b-4431-b70c-c6907f08b703" />


- Verify the database subnet/VM does **not** have a public IP address.
- Confirm that only the web tier is allowed to communicate with the database tier.
- Use network rules so the database remains inaccessible from the public internet.

 

**4. Review the virtual machine setup and access rules** [0:41](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=41)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cee5c00c-95b5-4e39-879c-b573b068909e" />

- Open **Virtual Machines** and confirm both VMs exist.
- Check that the web VM has the required public access for administration.
- Confirm the database VM is private and protected by access rules.
- Review any network/security rules that were created for the lab.

 

**5. Confirm the database VM only accepts traffic from the web subnet** [0:59](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=59)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/efd9c637-ff39-4746-b2f6-737cc389f037" />

- Verify the database VM is configured to allow traffic only from the **web subnet**.
- Ensure this rule supports remote access only from the web server.
- Confirm no other sources are permitted to connect to the database VM.

 

**6. Verify the web VM has the required public services exposed** [1:07](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=67)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e3d25ab0-7226-4fd8-9612-f6eb1c6c037e" />

- Confirm the web VM has a **public IP address**.
- Ensure the required ports are open: 
  - **Port 80** for web traffic
  - **Port 22** for SSH administration
- Validate that only necessary ports are exposed.

 

**7. SSH into the web server** [1:27](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=87)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/65bedab0-c329-4d4c-a483-aab81be2d46f" />

- Retrieve the SSH command for the web VM.
- Copy the web VM’s **public IP address**.
- Use SSH to connect to the web server from your admin workstation.
- Confirm you are successfully logged into the web VM.

 

**8. Test connectivity from the web server to the database server** [2:24](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=144)
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b19c3e80-4d94-4242-96f5-08a77f382a11" />

- From the web VM, obtain the **private IP address** of the database VM.
- Use a ping test or equivalent connectivity check from the web server to the database server.
- Confirm the database VM responds only over the private network path.

 

**9. Validate the secure two-tier design** [3:13](https://loom.com/share/41129e3a8c4345f19c3fb176b73dea64?t=193)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f4d54f61-0a38-4ef5-ab70-a220ac570ba8" />

- Confirm the web server can reach the database server using the private IP.
- Verify the database server remains inaccessible from public access.
- Document the result as proof that the two-tier web application is secure and functioning as intended.

### Cautionary Notes

- Do not assign a public IP address to the database VM.
- Avoid opening unnecessary ports on either VM.
- Ensure network rules are scoped as narrowly as possible so only the web tier can reach the database tier.
- Double-check that the private IP used for testing belongs to the database VM, not the web VM.

### Tips for Efficiency

- Keep the web and database subnet names simple and consistent for easier troubleshooting.
- Save the SSH command and IP addresses in a secure admin note for quick access.
- Verify network rules immediately after creation to avoid later connectivity issues.
- Test connectivity in this order: public access to web VM first, then private access from web VM to DB VM.
