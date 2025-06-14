## Deploying a Secure, Public Web Server on AWS

## Step 0: Create a Key Pair
![Key Pair](./images/keyPairs.png)

---

## Step 1: Create a VPC

- **Name:** `PriyeshRaiMinfy-vpc`
- **CIDR Block:** `10.0.0.0/16`

![VPC](./images/custom_VPC.png)

---

## Step 2: Create a Public Subnet

- **Name:** `PriyeshRaiMinfy-subnet`
- **CIDR Block:** `10.0.1.0/24`
- **Availability Zone:** `ap-south-1a` or first in list

![Subnet](./images/customSubnet.png)

---

## Step 3: Create and Attach Internet Gateway

- **Name:** `PriyeshRaiMinfy-igw`

![Internet Gateway Created](./images/iGw.png)

---

## Step 4: Configure Route Table

- **Action:** Add route `0.0.0.0/0` → `igw`

![Route Table](./images/rTable.png)

---

## Step 5: Create a Security Group

- **Name:** `PriyeshRaiMinfy-sg`
- **Inbound Rules:**
  - **SSH (22):** My IP
  - **HTTP (80):** Anywhere (0.0.0.0/0)
- **VPC:** `my-lab-vpc`

![Security Group](./images/secgroup.png)

---

## Step 6: Launch EC2 Instance

- **Instance Type:** `t2.micro`
- **Key Pair:** `PriyeshRaiMinfy-kp`
- **Network Settings:**
  - VPC: `PriyeshRaiMinfy-vpc`
  - Subnet: `PriyeshRaiMinfy-subnet`
  - Public IP: Enabled
  - Security Group: `PriyeshRaiMinfy-sg`

![EC2 Instance](./images/ec2instance1.png)

---

### -> User Data Script

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```

### Output
![Output](./images/output.png)

## Cleanup
![Output](./images/Screenshot%202025-06-11%20144230.png)
![Output](./images/Screenshot%202025-06-11%20144240.png)
![Output](./images/Screenshot%202025-06-11%20144246.png)
![Output](./images/Screenshot%202025-06-11%20144258.png)
![Output](./images/Screenshot%202025-06-11%20144332.png)
![Output](./images/Screenshot%202025-06-11%20144344.png)

