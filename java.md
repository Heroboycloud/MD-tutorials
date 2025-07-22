Installing **Java (JDK)** and **Javac** on **Windows 10 (32-bit)** is straightforward if you follow these steps carefully. Since 32-bit Windows has some limitations, you'll need to ensure you download the correct version of the JDK.

---

### **Step 1: Download the Correct JDK (32-bit)**
Since Oracle no longer provides **32-bit JDK** for newer versions, you have two options:

#### **Option 1: Oracle JDK 8 (32-bit)**
- **Download Link**:  
  [Oracle JDK 8u381 (32-bit)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html)  
  *(You may need an Oracle account to download.)*

#### **Option 2: OpenJDK (32-bit)**
- **Adoptium (Eclipse Temurin)**:  
  [https://adoptium.net/temurin/releases/](https://adoptium.net/temurin/releases/)  
  *(Check if they still offer 32-bit builds.)*

- **Azul Zulu (Community Edition)**:  
  [https://www.azul.com/downloads/?package=jdk](https://www.azul.com/downloads/?package=jdk)  
  *(Look for **x86 (32-bit)** versions.)*

---

### **Step 2: Install the JDK**
1. **Run the installer** (`jdk-8u381-windows-i586.exe` for Oracle JDK 8).  
2. Follow the installation wizard (keep default settings).  
3. **Note the installation path** (e.g., `C:\Program Files (x86)\Java\jdk1.8.0_381`).  

---

### **Step 3: Set Up Environment Variables**
To use `java` and `javac` from the command line, you must add them to **PATH**.

1. **Open System Properties**:
   - Press `Win + R`, type `sysdm.cpl`, and hit **Enter**.
   - Go to **Advanced** → **Environment Variables**.

2. **Add `JAVA_HOME`**:
   - Under **System Variables**, click **New**.
   - **Variable Name**: `JAVA_HOME`  
   - **Variable Value**: `C:\Program Files (x86)\Java\jdk1.8.0_381` *(adjust if different)*  
   - Click **OK**.

3. **Update `PATH`**:
   - Find **Path** in **System Variables**, click **Edit**.
   - Click **New** and add:  
     ```
     %JAVA_HOME%\bin
     ```
   - Click **OK** → **OK** → **OK**.

---

### **Step 4: Verify Installation**
1. **Open Command Prompt** (`Win + R` → `cmd`).  
2. Check `java` and `javac`:
   ```cmd
   java -version
   javac -version
   ```
   - If both show version numbers, **Java is installed correctly!**  
   - If not, restart your PC and try again.

---

### **Step 5: Write & Compile Your First Java Program**
1. **Create a file `HelloWorld.java`** (`Notepad` or any text editor):
   ```java
   public class HelloWorld {
       public static void main(String[] args) {
           System.out.println("Hello, World!");
       }
   }
   ```
2. **Save it** (e.g., `C:\Java\HelloWorld.java`).  
3. **Compile & Run**:
   ```cmd
   cd C:\Java
   javac HelloWorld.java
   java HelloWorld
   ```
   - Output should be: `Hello, World!`

---

### **Troubleshooting**
1. **"Java is not recognized"**  
   - Ensure `PATH` and `JAVA_HOME` are set correctly.  
   - Restart Command Prompt after changes.  

2. **32-bit vs. 64-bit Conflicts**  
   - If you see errors like `"Unable to access jarfile"`, ensure you installed the **32-bit JDK**.  

3. **Alternative: Use an IDE**  
   - **Eclipse (32-bit)**: [https://www.eclipse.org/downloads/](https://www.eclipse.org/downloads/)  
   - **IntelliJ IDEA (Community Edition)**: [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/)  
     *(Check if they support 32-bit.)*

---

### **Final Notes**
- **Java