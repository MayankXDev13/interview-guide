## Question  
Can you restore a lost PEM file? If not, how can you still access the EC2 instance?

### Short Explanation  
This question evaluates your knowledge of secure SSH access, key-based authentication, and how to regain access to EC2 instances when your only login method (PEM file) is lost.

## Answer  
No, you **cannot restore** a lost PEM file — it’s not stored on AWS or recoverable.  
However, you can **regain access** by using a workaround: create a new key pair, attach it to the instance via a temporary EC2 rescue process, and restore SSH access.

### Detailed Explanation  

PEM files (private keys) are **never retrievable from AWS** after initial creation. Losing the PEM file means you cannot SSH into the EC2 instance using the existing key pair.

But here’s how you can still regain access:




------------------------------------------------------------------------

#### Step 1: Generate a New SSH Key Pair (Recommended)

Generate a new ED25519 key pair on your local machine:

``` bash
ssh-keygen -t ed25519 -f my-key.pem
chmod 400 my-key.pem
```

This creates:

``` text
my-key.pem       # Private key
my-key.pem.pub   # Public key
```

------------------------------------------------------------------------

## Step 2: Stop the Original EC2 Instance

``` bash
aws ec2 stop-instances --instance-ids i-xxxxxxxxxxxxxxxxx
```

Wait until the instance is fully stopped.

------------------------------------------------------------------------

## Step 3: Detach the Root EBS Volume

1.  Open the AWS Console.
2.  Navigate to **EC2 → Volumes**.
3.  Select the root volume attached to the affected instance.
4.  Detach the volume.

------------------------------------------------------------------------

## Step 4: Launch a Temporary EC2 Instance

Create a helper instance in the **same Availability Zone** as the
original instance.

------------------------------------------------------------------------

## Step 5: Attach the Detached Volume

Attach the detached root volume to the helper instance as a secondary
volume (for example, `/dev/sdf`).

------------------------------------------------------------------------

## Step 6: Identify and Mount the Partition

Identify the Linux partition:

``` bash
lsblk -f
```

If needed:

``` bash
sudo fdisk -l
```

Create a mount point and mount the correct partition (example):

``` bash
sudo mkdir -p /mnt/recovery
sudo mount /dev/xvdf1 /mnt/recovery
```

> Replace `/dev/xvdf1` with the correct partition shown by `lsblk`.

------------------------------------------------------------------------

## Step 7: Add the New Public Key

Display your public key:

``` bash
cat my-key.pem.pub
```

Append it to the original instance's `authorized_keys`.

For Ubuntu:

``` bash
sudo mkdir -p /mnt/recovery/home/ubuntu/.ssh
sudo nano /mnt/recovery/home/ubuntu/.ssh/authorized_keys
```

Paste the contents of `my-key.pem.pub`, or append it directly:

``` bash
cat my-key.pem.pub | sudo tee -a /mnt/recovery/home/ubuntu/.ssh/authorized_keys
```

### Set Correct Permissions

``` bash
sudo chmod 700 /mnt/recovery/home/ubuntu/.ssh
sudo chmod 600 /mnt/recovery/home/ubuntu/.ssh/authorized_keys
sudo chown -R ubuntu:ubuntu /mnt/recovery/home/ubuntu/.ssh
```

### Common Default SSH Users

  Operating System   SSH User              Home Directory
  ------------------ --------------------- ---------------------------------
  Ubuntu             `ubuntu`              `/home/ubuntu`
  Amazon Linux       `ec2-user`            `/home/ec2-user`
  Debian             `admin` or `debian`   `/home/admin` or `/home/debian`
  Rocky Linux        `rocky`               `/home/rocky`
  CentOS             `centos`              `/home/centos`

------------------------------------------------------------------------

## Step 8: Unmount the Volume

``` bash
sudo umount /mnt/recovery
```

Detach the volume from the helper instance.

------------------------------------------------------------------------

## Step 9: Reattach the Volume

Attach the volume back to the original EC2 instance using its original
root device name (for example, `/dev/xvda`).

------------------------------------------------------------------------

## Step 10: Start the Original Instance

``` bash
aws ec2 start-instances --instance-ids i-xxxxxxxxxxxxxxxxx
```

------------------------------------------------------------------------

## Step 11: Connect Using the New Key

Ubuntu:

``` bash
ssh -i my-key.pem ubuntu@<PUBLIC_IP>
```

Amazon Linux:

``` bash
ssh -i my-key.pem ec2-user@<PUBLIC_IP>
```

------------------------------------------------------------------------
