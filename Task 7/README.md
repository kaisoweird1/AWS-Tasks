# AMI Creation, Snapshots, and AWS EBS Volume Attachment

AWS resources are frequently backed up and replicated across instances using **EBS Volumes**, **Snapshots**, and **AMIs** for better data management and replication. Attaching a **EBS Volume** to an EC2 instance, taking **Snapshots** of the volume to preserve data, and producing a **AMI (Amazon Machine Image)** to record the complete instance configuration are the steps involved in this task.


While the AMI contains the EC2 instance's operating system and configurations, the snapshots maintain the volume's state. Once an AMI has been created, it can be used to launch new EC2 instances, guaranteeing simple replication, disaster recovery, and scalability.

This method enhances **data durability**, **instance management**, and offers a reliable means of recovering or replicating environments by utilizing **Snapshots** and **AMIs**.

## 1) Create an Instance and add a file to it
## 2) Create a snapshot of this instance
![WhatsApp Image 2025-06-05 at 23 44 25_021e4da9](https://github.com/user-attachments/assets/4e532f15-2db9-4760-8713-c147b356c568)

## 3) Using this snapshot, create a volume
![WhatsApp Image 2025-06-05 at 23 46 50_d46412f0](https://github.com/user-attachments/assets/800767b1-fd91-4d0e-b655-495c3358061e)

## 4) Attach this newly created volume to the second instance that you create
![WhatsApp Image 2025-06-05 at 23 58 57_98250521](https://github.com/user-attachments/assets/92a3b4bc-5779-4932-aeac-b54eee656495)

## 5) Mount the volume onto this instance and check for the file you added to the first instance
![WhatsApp Image 2025-06-06 at 00 22 40_90b2b9c3](https://github.com/user-attachments/assets/aa621909-e151-4549-838b-e7503cc217fb)

## 6) Create an AMI using the first instance
![WhatsApp Image 2025-06-06 at 00 50 34_aaf20a3b](https://github.com/user-attachments/assets/eaffd3b1-30d1-4885-a6a4-eea9f1a8e950)
## 7) Create an instance using this AMI 
![WhatsApp Image 2025-06-06 at 00 51 44_4bdbe935](https://github.com/user-attachments/assets/777a3805-3cc5-4ce7-a30d-cb72d46fa845)
## 8) Check for the file in this new instance
![WhatsApp Image 2025-06-06 at 00 50 01_83ad31cc](https://github.com/user-attachments/assets/1a8d251d-4ba7-40e7-8c8c-ba2f57058d2b)




