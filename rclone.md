# Introducing rclone
Rclone is free open source software that can copy or sync two file locations, where any changes will be moved between each. Install rclone by downloading it from [rclone's official website](https://rclone.org/downloads/). 

There is no install, just put the rclone software someplace that you will remember. I put it in the directory `C:\cmds\rclone`. If this is not part of the windows path, you must use the full path in the command line. For example, `c:\cmds\rclone\rclone.exe -options'. 

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

The `copy` option is a safer option if you want to avoid accidentally deleting files in the destination, while `sync` is used for creating an exact replica of the source, which includes deleting files in the destination that are no longer present in the source.

## Using `rclone` to Copy from a USB key or drive to your personal computer:

Using `rclone` to copy data from a USB key to your hard drive is quite straightforward. This is a COPY command only, it does not sync the files. 

1. **Identify your USB Key and Hard Drive Paths:**
   - Plug in your USB key.
   - Identify the mount path of your USB key and the destination path on your hard drive. This can be done using a file manager or command line tools. For example in Windows, the USB key might be mounted at `E:\`, and you might want to copy files to `C:\Users\YourName\DestinationFolder`.

2. **Open a Command Line Interface:**
   - On Windows, open Command Prompt or PowerShell. Type "command" in the start menu to start this.

3. **Run the rclone copy command:**
   - The basic syntax for the rclone copy command is `rclone copy source:path dest:path`.
   - For example, if your USB key is mounted at `E:\` and you want to copy its contents to a folder at `C:\Users\YourName\DestinationFolder`, the command would be:
     ```
     rclone copy E:\ C:\Users\YourName\DestinationFolder
     ```

4. **Execute the Command:**
   - After typing the command, press Enter.
   - rclone will start copying the files from your USB key to the specified folder on your hard drive.
   - You can do a dry run of this by adding the flag --dry-run at the end. This way you can see what it will do before it actually does it!

5. **Verify the Copy:**
   - Once the process is complete, verify that the files have been copied to the destination folder.
   - If using the dry run, actually do the command!

Remember, these instructions are for a basic copy operation. rclone has many advanced features and options which you can explore in its documentation if needed.

## Creating a batch file to sync a USB Key with OneDrive (or other cloud provider)

Creating a Windows batch script to sync a local folder with a OneDrive account using `rclone` involves a few steps:

### Prerequisites - set up the authentication:

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

## Best Practices and Tips

Using `rclone` effectively and safely involves following some best practices. These practices help ensure data integrity, security, and efficient operation:

1. **Understand Sync vs Copy:**
   - Understand the difference between `sync` and `copy` commands. `sync` makes the destination exactly the same as the source, potentially deleting files in the destination, while `copy` just copies new or updated files from the source to the destination.

2. **Test with Small Data Sets First:**
   - Before running large or important syncs, test your commands with a small, non-critical dataset to ensure they work as expected.

3. **Use Verbose or Dry-Run Modes for Troubleshooting:**
   - Use the `--dry-run` or `--verbose` flag to test your commands without making any changes. This helps in understanding what rclone will do.

4. **Check Bandwidth Usage:**
   - Be mindful of bandwidth usage, especially if you have a limited internet plan. Use the `--bwlimit` flag to limit bandwidth usage.

5. **Configure Filters Appropriately:**
   - Use filters to include or exclude specific files or directories. Carefully check your filter rules to avoid syncing unwanted files.
   - Be aware of the rate limits and API quotas of your storage provider to avoid hitting these limits.

6. **Secure Your Config File:**
   - The rclone config file contains sensitive information. Secure it by setting appropriate file permissions and consider using the `--password-command` feature for additional security.

7. **Use Crypt for Sensitive Data:**
   - If you're syncing sensitive data, consider using rclone’s crypt feature to encrypt files before uploading.

8. **Automate and Schedule Backups:**
    - For regular backups, automate and schedule your rclone tasks with cron jobs (Linux) or Task Scheduler (Windows).

9. **Be Careful with Delete Operations:**
    - Be very cautious with commands that delete data (`sync`, `delete`, etc.). Double-check the paths and flags to prevent accidental data loss.

Following these practices will help ensure that you use rclone effectively and safely, minimizing the risk of data loss or other issues.
