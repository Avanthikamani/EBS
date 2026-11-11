# WORKING WITH EBS
## NAME: DEVENDRAN G
## REG NO: 212225240030

## Aim

To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

---

## Algorithm / Steps

1. Create a new Amazon EBS volume with a size of 1 GiB.
2. Select the same Availability Zone as the EC2 instance.
3. Attach the EBS volume to the EC2 instance using `/dev/sdb`.
4. Connect to the EC2 instance using AWS Systems Manager Session Manager.
5. Check the available storage using `df -h`.
6. Create an `ext3` file system on the EBS volume.
7. Create the `/mnt/data-store` directory.
8. Mount the EBS volume to `/mnt/data-store`.
9. Configure `/etc/fstab` for automatic mounting.
10. Verify that the EBS volume is successfully mounted.
11. Create `file.txt` inside the mounted EBS volume.
12. Verify the contents of the created file.
13. Create an EBS snapshot named `My Snapshot`.
14. Delete `file.txt` from the original EBS volume.
15. Create a new EBS volume from the snapshot.
16. Attach the restored volume to the EC2 instance using `/dev/sdc`.
17. Create the `/mnt/data-store2` directory.
18. Mount the restored volume to `/mnt/data-store2`.
19. Verify that `file.txt` has been successfully restored.

---

## Program

### 1. Check Available Storage

```bash
df -h
```

### 2. Create an ext3 File System

```bash
sudo mkfs -t ext3 /dev/sdb
```

### 3. Create a Mount Directory

```bash
sudo mkdir /mnt/data-store
```

### 4. Mount the EBS Volume

```bash
sudo mount /dev/sdb /mnt/data-store
```

### 5. Configure Automatic Mounting

```bash
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### 6. View the File System Configuration

```bash
cat /etc/fstab
```

### 7. Verify the Mounted Volume

```bash
df -h
```

### 8. Create a File in the EBS Volume

```bash
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

### 9. Read the File

```bash
cat /mnt/data-store/file.txt
```

### 10. Delete the File

```bash
sudo rm /mnt/data-store/file.txt
```

### 11. Verify File Deletion

```bash
ls /mnt/data-store/
```

### 12. Create a Mount Directory for the Restored Volume

```bash
sudo mkdir /mnt/data-store2
```

### 13. Mount the Restored EBS Volume

```bash
sudo mount /dev/sdc /mnt/data-store2
```

### 14. Verify Snapshot Restoration

```bash
ls /mnt/data-store2/
```

Expected output:

```text
file.txt
```

---

## Outputs
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/23bbd1c7-502b-4d19-9a68-dc7c8e7a7ef4" />
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/4b0a89d0-d4e6-4286-8b63-17975714e392" />
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/d6bbe90e-11f9-445c-a846-6e3ce6b4f271" />
<img width="1400" height="630" alt="image" src="https://github.com/user-attachments/assets/bac683ec-7c40-456c-b439-62a20a7fa019" />
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/00a3a786-bc7a-490d-8c2a-5cfa7a35e47c" />
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/620c7487-4f88-40b1-9762-6ec998213183" />
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/293a167d-1d31-451a-87c5-09a3aab24782" />
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/94cbb94e-176d-44c8-8344-4b4f6bbae3ca" />
<img width="630" height="1400" alt="image" src="https://github.com/user-attachments/assets/46bca885-aea6-4672-9967-3e5f454e0970" />
<img width="1400" height="630" alt="image" src="https://github.com/user-attachments/assets/2ac797d7-4c34-4947-aac6-051577d4a76b" />



## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.
