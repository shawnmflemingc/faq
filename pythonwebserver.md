# Using Python as a Web Server for Static Files

To host a website from a specific directory using Python 3, you can use the built-in HTTP server module that comes with Python. This method is great for testing or development purposes but is not recommended for production use due to security and performance reasons.

### Finding ArcGIS Pro's Python Install Directory

Typing "python" in command prompt likely will not work. You must use a full path to specify where python.exe is found. ArcGIS Pro uses its own Python environment, which is typically a version of Python 3.x that's managed by the ArcGIS Pro application and can be used for simple purposes like this. To find the directory of the Python executable used by ArcGIS Pro, you can follow these steps:

1. **Open ArcGIS Pro**: Start ArcGIS Pro on your computer.

2. **Open the Python Window**: This can usually be done from the "Analysis" tab by clicking on "Python" to open the Python window.

3. **Run a Python Command**: In the Python window, you can run a command to display the path to the Python executable. Type the following command and press Enter:
   
   ```python
   import sys
   print(sys.executable)
   ```

   This command will print the full path to the Python executable that ArcGIS Pro is using.

4. **Note the Path**: The printed path is the location of the Python executable. It will typically be something like:
   
   ```
   C:\Program Files\ArcGIS\Pro\bin\Python\envs\arcgispro-py3\python.exe
   ```

   The exact path may vary depending on the version of ArcGIS Pro and your installation directory.

5. **Use the Python Environment**: You can use this executable to run Python scripts that require ArcGIS Pro's Python environment and will work fine for the purposes of running a static HTTP server. 

Having your Python environment now you can run a web server:

### Step 1: Prepare Your Website Files
- Make sure all your website files (HTML, CSS, JavaScript, images, etc.) are placed in the directory you want to serve. Let's say this directory is `C:\path\to\your\website`.

### Step 2: Open Command Prompt or Terminal
- Open Command Prompt (start menu then type in `Command Prompt`, or run `cmd`)

### Step 3: Navigate to Your Directory
- Use the `cd` command to navigate to your website directory. It is important to be in the correct directory since that is what will host your files. Check using `dir` to list the files in the current directory in command prompt.
  ```bash
  cd C:\path\to\your\website
  ```

### Step 4: Start Python HTTP Server
- In your command prompt or terminal, run the following command (be sure to include the full path to the python.exe file):
  ```bash
  "C:\Your\Path\python.exe" -m http.server
  ```
- By default, this will host your website on port 8000 using the files located in the current directory. If you need to use a different port and want to use the default path for ArcGIS Pro's Python, you can specify it by adding the port number at the end of the command, like this:
  ```bash
  "C:\Program Files\ArcGIS\Pro\bin\Python\envs\arcgispro-py3\python.exe" -m http.server 8080
  ```

### Step 5: Access Your Website
- Open your web browser and go to `http://localhost:8000` (or whichever port you chose).
- You should see your website served from the directory you specified.

### Notes:
  
1. **Security Warning**: The built-in Python HTTP server is not secure for production use. It's only intended for development and testing. If you plan to host a website publicly, consider using a proper web server or a hosting service.

2. **Dynamic Content**: This server serves static files. If your website needs to handle dynamic content, you'll need a more complex setup, like a web framework (e.g., Flask or Django).

Remember, when you close the command prompt or terminal, the server will stop running. This is a simple and quick way to serve static files for testing or development purposes.
