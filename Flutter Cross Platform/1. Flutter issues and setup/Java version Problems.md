___
## how to change the java version in my system to java 21?
### **1. Check Current Java Version**
First, verify your current Java version:
```
java -version
```
---
### **2. Install Java 21**
#### **Windows**:

1. Download the JDK 21 installer from [Oracle](https://www.oracle.com/java/technologies/downloads/).
    
2. Run the installer and follow the prompts.
    
3. Note the installation path (e.g., `C:\Program Files\Java\jdk-21`).
---
### **3. Set Java 21 as Default**
#### **Windows**:

1. Open **System Properties** > **Environment Variables**.
    
2. Under **System Variables**, edit `JAVA_HOME` to point to the JDK 21 path (e.g., `C:\Program Files\Java\jdk-21`).
    
3. Update the `Path` variable to include `%JAVA_HOME%\bin`.
    

---
### **4. Verify the Change**
Check if Java 21 is now the default:
bash
```
java -version
```
---

### **Troubleshooting**
### **Step-by-Step Fix for Windows**

1. **Check `JAVA_HOME`**:
```
echo %JAVA_HOME%
```
2. **Update `JAVA_HOME`**:
      
3. **Fix the `Path` Variable**:
    - Ensure the entry for Java 21’s `bin` directory (e.g., `%JAVA_HOME%\bin`) is placed **above** any entries for Java 23.  
        ⚠️ Windows uses the **first valid path** it finds, so Java 21’s path must appear **before** Java 23’s path.
4. **Remove Java 23 Entries (Optional)**:
    - If you no longer need Java 23, delete its entries from the `Path` variable and uninstall it via **Control Panel > Programs > Uninstall a Program**.
5. **Restart Command Prompt**:
```
java -version
```
___
### **Example Fix**

If `where java` shows:

Copy

C:\Program Files\Java\jdk-23\bin\java.exe   <--- Problem!
C:\Program Files\Java\jdk-21\bin\java.exe

1. Delete the Java 23 entry from `Path`.
    
2. Add Java 21’s `bin` path to the top of `Path`.
___
### Purpose of the Command:

1. **Set the JDK Path**:
    
    - Flutter uses the JDK for tasks related to building and running Android apps, such as compiling the code, signing APKs, and interacting with Android tools.
    - This command explicitly tells Flutter where to find the installed JDK on your system.
2. **Resolve Environment Issues**:
    
    - If the JDK is not in your system's environment `PATH` or if you have multiple JDK versions installed, this command ensures Flutter uses the correct one.
3. **Improve Build Consistency**:
    
    - By explicitly setting the JDK directory, you eliminate the risk of Flutter picking up an incorrect or incompatible JDK version.
```
flutter config --jdk-dir="C:\Program Files\Java\jdk-20"
```