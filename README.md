# WORKING WITH EBS
## NAME: AVANTHIKA.M
## REG NO: 212224110009

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
<img width="1917" height="1031" alt="Screenshot 2026-11-03 091105" src="https://github.com/user-attachments/assets/fb9a93f2-9d89-48a3-a4a2-1ef4a9cf481d" />
<img width="1916" height="1037" alt="Screenshot 2026-11-08 081725" src="https://github.com/user-attachments/assets/8a09cf17-e224-42d5-af5c-ac5215a8d7db" />
<img width="1917" height="1022" alt="Screenshot 2026-11-08 081816" src="https://github.com/user-attachments/assets/1f25f31c-417a-4f81-99b1-8720e6a3694a" />
<img width="1917" height="1042" alt="Screenshot 2026-11-08 082031" src="https://github.com/user-attachments/assets/ef24e292-3371-476f-89a1-0747313a6eca" />
<img width="1917" height="1027" alt="Screenshot 2026-11-08 082101" src="https://github.com/user-attachments/assets/57a57715-2e91-4fa1-a0e2-2ac955047cf1" />
<img width="1915" height="1028" alt="Screenshot 2026-11-08 082302" src="https://github.com/user-attachments/assets/8f66cfaf-7f4b-4e2d-b852-fe5574c4ecd8" />
<img width="1917" height="1032" alt="Screenshot 2026-11-08 082321" src="https://github.com/user-attachments/assets/0751b0db-1369-4157-aea9-69f120f26c12" />





## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.
