# webservicedeplolyment


# Static Website on Azure VM

This project provides a step-by-step guide to create a static website hosted on an Azure Virtual Machine (VM). It includes the use of a Linux-based VM, configuration of a web server, and optional enhancements like integrating a CDN using Azure Front Door and automating the process with Terraform.

## Prerequisites

- Azure account with subscription
- Basic knowledge of using the Azure portal and command-line tools
- SSH client installed on your machine
- (Optional) Terraform installed for automation

## Steps

### 1. Create an Azure Virtual Machine

1. **Log in to the Azure Portal**:  
   [Azure Portal](https://portal.azure.com/)

2. **Create a Resource Group**:  
   - Navigate to **Resource Groups** and create a new group (e.g., `StaticWebsiteRG`).

3. **Set up a Virtual Network (VNet)**:  
   - Create a VNet (e.g., `VNetStaticWebsite`) with a subnet (e.g., `WebSubnet`).

![image](https://github.com/user-attachments/assets/b64b9bbd-037f-4ea8-96a5-fef3df826393)

4. **Deploy the Virtual Machine**:  
   - Choose Ubuntu or any Linux distribution as the image.
   - Ensure HTTP (port 80) traffic is allowed in the network security group (NSG).

5. **Configure Network Security**:  
   - Create an NSG and allow inbound HTTP traffic.
   - Attach the NSG to the VM's subnet.
![image](https://github.com/user-attachments/assets/4608c0ce-ca2b-414a-84b8-d3bd1e93bba9)

### 2. Install and Configure a Web Server

1. **Access the Virtual Machine**:  
   - Use SSH: `ssh <username>@<VM_Public_IP>`.

2. **Install Apache**:  
   ```bash
   sudo apt update
   sudo apt install apache2 -y
   ```

3. **Add Website Content**:  
   - Update the HTML file:  
     ```bash
     sudo nano /var/www/html/index.html
     ```
   - Add your HTML content (e.g., "Hello World!").
![image](https://github.com/user-attachments/assets/1f827c27-183b-472b-8efd-5acdb7270b91)

4. **Restart the Web Server**:  
   ```bash
   sudo systemctl restart apache2
   ```

5. **Test the Website**:  
   - Open the VM's public IP in a browser.
![image](https://github.com/user-attachments/assets/b2ca879b-091e-43a6-aa2b-22daa9d32a41)

### 3. Optional Enhancements

#### Add a CDN Using Azure Front Door

1. Create a Front Door profile.
   ![image](https://github.com/user-attachments/assets/4f5be451-b878-4698-a4a2-f561134b88c2)

2. Configure it to route traffic to the VM's public IP.
![image](https://github.com/user-attachments/assets/122e6145-e2ad-4f7a-9a4b-ce30047954fe)

#### Automate Deployment with Terraform

1. **Install Terraform**:  
   - [Download Terraform](https://www.terraform.io/downloads.html)

2. **Create a `main.tf` File**:  
   - Include configurations for resource group, VNet, NSG, and VM.

3. **Deploy with Terraform**:  
   ```bash
   terraform init
   terraform apply
   ```

## Project Structure

```
/
├── main.tf        # Terraform configuration file (optional)
├── README.md      # This documentation
```

## Resources

- [Azure Portal](https://portal.azure.com/)
- [Terraform Documentation](https://www.terraform.io/docs/)

## License

This project is licensed under the MIT License.
