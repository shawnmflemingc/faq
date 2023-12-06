# Introducing rclone
Rclone is free open source software that can copy or sync two file locations, where any changes will be moved between each. Install rclone by downloading it from [rclone's official website](https://rclone.org/downloads/). 

In `rclone`, the `sync` and `copy` commands are used for transferring files between file systems, but they operate differently:

1. **Copy Command:**
   - **Function**: The `copy` command copies files from the source to the destination.
   - **Key Behavior**: 
     - Only new and updated files are copied over.
     - It does not delete any files from the destination that are not present in the source.
     - If a file exists in both the source and the destination, it will only be copied if the source version is newer or differs in size.
   - **Use Case**: Ideal for backing up files where you want to retain all files in the destination, even if they have been removed from the source.

2. **Sync Command:**
   - **Function**: The `sync` command makes the destination identical to the source by copying and deleting as necessary.
   - **Key Behavior**: 
     - Like `copy`, it copies new and updated files to the destination.
     - Additionally, it deletes any files from the destination that are not present in the source.
     - The destination becomes an exact mirror of the source after the operation.
   - **Use Case**: Ideal for maintaining an exact copy of a source folder. Use with caution, as it can result in data loss in the destination if files are removed from the source.

In summary, `copy` is a safer option if you want to avoid accidentally deleting files in the destination, while `sync` is used for creating an exact replica of the source, which includes deleting files in the destination that are no longer present in the source.

## Using `rclone` to Copy from a USB key or drive to your personal computer:

Using `rclone` to copy data from a USB key to your hard drive is quite straightforward. This is a COPY command only, it does not sync the files. 

1. **Identify your USB Key and Hard Drive Paths:**
   - Plug in your USB key.
   - Identify the mount path of your USB key and the destination path on your hard drive. This can be done using a file manager or command line tools. For example, the USB key might be mounted at `E:\` (Windows) or `/media/usbkey` (Linux), and you might want to copy files to `C:\Users\YourName\DestinationFolder` (Windows) or `/home/yourname/destinationfolder` (Linux).

2. **Open a Command Line Interface:**
   - On Windows, open Command Prompt or PowerShell.
   - On macOS or Linux, open Terminal.

3. **Run the rclone copy command:**
   - The basic syntax for the rclone copy command is `rclone copy source:path dest:path`.
   - For example, if your USB key is mounted at `/media/usbkey` and you want to copy its contents to a folder at `/home/yourname/destinationfolder`, the command would be:
     ```
     rclone copy /media/usbkey /home/yourname/destinationfolder
     ```
   - If you're using Windows and your USB key is on `E:\` and you want to copy to `C:\Users\YourName\DestinationFolder`, the command would be:
     ```
     rclone copy E:\ C:\Users\YourName\DestinationFolder
     ```

4. **Execute the Command:**
   - After typing the command, press Enter.
   - rclone will start copying the files from your USB key to the specified folder on your hard drive.

5. **Verify the Copy:**
   - Once the process is complete, verify that the files have been copied to the destination folder.

Remember, these instructions are for a basic copy operation. rclone has many advanced features and options which you can explore in its documentation if needed.

## Creating a batch file to sync a USB Key with OneDrive

Creating a Windows batch script to sync a local folder with a OneDrive account using `rclone` involves a few steps:

### Prerequisites:

1. **Set up rclone with OneDrive**: 
   - Run `rclone config` in the command line.
   - Follow the prompts to add a new remote of the type `OneDrive`.
   - Complete the authentication process for OneDrive.

2. **Identify Local and Remote Paths**: 
   - Decide the local folder path you want to sync (e.g., `C:\Users\YourName\LocalFolder`).
   - Note the name you assigned to your OneDrive remote during the setup process (e.g., `onedrive`).

### Batch Script:

1. Open Notepad or any text editor.

2. Copy and paste the following script:

    ```batch
    @echo off
    SETLOCAL

    set "RCLONE_PATH=C:\path\to\rclone.exe"
    set "LOCAL_PATH=C:\Users\YourName\LocalFolder"
    set "REMOTE_PATH=onedrive:FolderOnOneDrive"

    echo Syncing from %LOCAL_PATH% to %REMOTE_PATH%...
    %RCLONE_PATH% sync "%LOCAL_PATH%" "%REMOTE_PATH%" --progress

    echo Sync complete.
    pause
    ```

    Replace `C:\path\to\rclone.exe` with the actual path to your `rclone.exe`. Adjust `LOCAL_PATH` and `REMOTE_PATH` with your local folder path and OneDrive folder path, respectively.

3. Save the file with a `.bat` extension, for example, `OneDriveSync.bat`.

4. To run the script, double-click on the `.bat` file.

### Notes:

- This script will sync the contents of the local folder to the specified folder in OneDrive. If a file in the local folder is deleted, it will also be deleted in the OneDrive folder during sync.

- Make sure you test the script with non-critical data first to ensure it works as expected and to prevent accidental data loss.

- The `--progress` flag in the script displays real-time progress. You can remove this flag or replace it with other `rclone` flags as needed.

- The `pause` command at the end keeps the command window open so you can see any messages or errors after the sync completes.

## Best Practices

Using `rclone` effectively and safely involves following some best practices. These practices help ensure data integrity, security, and efficient operation:

1. **Understand Sync vs Copy:**
   - Understand the difference between `sync` and `copy` commands. `sync` makes the destination exactly the same as the source, potentially deleting files in the destination, while `copy` just copies new or updated files from the source to the destination.

2. **Test with Small Data Sets First:**
   - Before running large or important syncs, test your commands with a small, non-critical dataset to ensure they work as expected.

3. **Regularly Update rclone:**
   - Keep rclone updated to benefit from the latest features, bug fixes, and security patches.

4. **Use Verbose or Dry-Run Modes for Troubleshooting:**
   - Use the `--dry-run` or `--verbose` flag to test your commands without making any changes. This helps in understanding what rclone will do.

5. **Check Bandwidth Usage:**
   - Be mindful of bandwidth usage, especially if you have a limited internet plan. Use the `--bwlimit` flag to limit bandwidth usage.

6. **Configure Filters Appropriately:**
   - Use filters to include or exclude specific files or directories. Carefully check your filter rules to avoid syncing unwanted files.

7. **Monitor Log Files:**
   - Keep log files for your transfers (using `--log-file` option), especially for automated scripts. This helps in troubleshooting and audit trails.

8. **Secure Your Config File:**
   - The rclone config file contains sensitive information. Secure it by setting appropriate file permissions and consider using the `--password-command` feature for additional security.

9. **Use Crypt for Sensitive Data:**
   - If you're syncing sensitive data, consider using rclone’s crypt feature to encrypt files before uploading.

10. **Understand the Limits of Your Storage Provider:**
    - Be aware of the rate limits and API quotas of your storage provider to avoid hitting these limits.

11. **Automate and Schedule Backups:**
    - For regular backups, automate and schedule your rclone tasks with cron jobs (Linux) or Task Scheduler (Windows).

12. **Use the Latest Stable Version:**
    - Always use the latest stable version of rclone for the best performance and security.

13. **Backup Configuration Files:**
    - Regularly back up your rclone configuration files, especially when you have complex setups.

14. **Be Careful with Delete Operations:**
    - Be very cautious with commands that delete data (`sync`, `delete`, etc.). Double-check the paths and flags to prevent accidental data loss.

15. **Keep an Eye on Quotas:**
    - Monitor your cloud storage quotas to avoid issues with storage limits.

16. **Regularly Review Access Permissions:**
    - Regularly review and audit the access permissions you have set on your cloud storage to ensure they remain secure and appropriate.

Following these practices will help ensure that you use rclone effectively and safely, minimizing the risk of data loss or other issues.
