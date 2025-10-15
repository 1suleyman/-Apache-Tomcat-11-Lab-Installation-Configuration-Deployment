# ☕ Apache Tomcat 11 Lab – Installation, Configuration & Deployment

In this lab, I learned how to **install, configure, and deploy web applications** on the **Apache Tomcat 11** server. I practiced setting up Tomcat on a Linux system, changing its default port, locating key directories, and deploying a `.war` application.

---

## 📋 Lab Overview

**Goal:**

* Download, extract, and configure Apache Tomcat 11
* Start and stop Tomcat services on Linux
* Change Tomcat’s default port
* Deploy and verify a sample `.war` web application

**Learning Outcomes:**

* Install and configure Tomcat in `/opt` directory
* Use `startup.sh` and `shutdown.sh` scripts
* Understand Tomcat folder structure and logs
* Deploy `.war` apps inside the `webapps` directory
* Verify successful deployment through a browser or terminal

---

## 🛠 Step-by-Step Journey

### **Step 1: Download Apache Tomcat 11**

**Task:** Download the latest Apache Tomcat 11 archive (from the `bin/` directory).

```bash
sudo wget https://downloads.apache.org/tomcat/tomcat-11/v11.0.13/bin/apache-tomcat-11.0.13.tar.gz
```

💡 The `wget` command fetches files from a remote URL.
✅ File `apache-tomcat-11.0.13.tar.gz` downloaded successfully.

---

### **Step 2: Extract the Archive**

```bash
sudo tar -xvf apache-tomcat-11.0.13.tar.gz
```

✅ Extracted the Tomcat package successfully.

---

### **Step 3: Move Extracted Files to /opt Directory**

```bash
sudo mv apache-tomcat-11.0.13 /opt/apache-tomcat-11
```

💡 Following naming conventions (use only the **major version** for consistency).
✅ Tomcat files now located at `/opt/apache-tomcat-11`.

---

### **Step 4: Verify Installation Path**

```bash
ls -l /opt/apache-tomcat-11
```

✅ Confirmed Tomcat directory structure (`bin`, `conf`, `webapps`, `logs`, etc.)

---

### **Step 5: Start Tomcat Server (Linux)**

```bash
sudo /opt/apache-tomcat-11/bin/startup.sh
```

💡 `startup.sh` launches Tomcat using Java.
✅ Tomcat successfully started — verified via localhost page.

---

### **Step 6: Start/Stop Scripts (Linux vs Windows)**

| OS      | Start Script  | Stop Script    |
| ------- | ------------- | -------------- |
| Linux   | `startup.sh`  | `shutdown.sh`  |
| Windows | `startup.bat` | `shutdown.bat` |

✅ Both verified.

---

### **Step 7: Change Default Tomcat Port (8080 → 9090)**

Edit the configuration using `sed` command to replace port number:

```bash
sudo sed -i 's/8080/9090/g' /opt/apache-tomcat-11/conf/server.xml
```

Restart Tomcat to apply changes:

```bash
sudo /opt/apache-tomcat-11/bin/shutdown.sh
sudo /opt/apache-tomcat-11/bin/startup.sh
```

✅ Tomcat now accessible on **port 9090** (e.g., `localhost:9090`).

Verify Tomcat process and status:

```bash
curl localhost:9090
ps -ef | grep tomcat
```

✅ Confirmed Tomcat running on new port.

---

### **Step 8: Locate Tomcat Logs and Webapps Directory**

| Directory                       | Description                                   |
| ------------------------------- | --------------------------------------------- |
| `/opt/apache-tomcat-11/logs`    | Stores Tomcat logs (including `catalina.out`) |
| `/opt/apache-tomcat-11/webapps` | Folder where `.war` files are deployed        |

✅ Verified both directories exist.

---

### **Step 9: Deploy the Sample Application**

**Task:** Deploy the provided `sample.war` file.

```bash
sudo mv /opt/sample.war /opt/apache-tomcat-11/webapps/
```

✅ The `.war` file was moved to the correct deployment directory.

**Restart Tomcat:**

```bash
sudo /opt/apache-tomcat-11/bin/startup.sh
```

**Verify Deployment:**
Access the app via:

```
http://localhost:9090/sample/index.html
```

✅ The browser displayed **“Hello World”** — confirming successful deployment.

---

### **Step 10: Identify Deployment Log File**

**Question:** Which log file records `.war` extraction and deployment details?
**Answer:**

```
catalina.out
```

✅ `catalina.out` contains deployment logs, including extraction of `.war` files.

🏁 **End of Lab**

---

## ✅ Key Commands Summary

| Task              | Command                                                             |
| ----------------- | ------------------------------------------------------------------- |
| Download Tomcat   | `sudo wget <URL>`                                                   |
| Extract archive   | `sudo tar -xvf <filename>.tar.gz`                                   |
| Move folder       | `sudo mv apache-tomcat-* /opt/apache-tomcat-11`                     |
| Start Tomcat      | `sudo /opt/apache-tomcat-11/bin/startup.sh`                         |
| Stop Tomcat       | `sudo /opt/apache-tomcat-11/bin/shutdown.sh`                        |
| Change port       | `sudo sed -i 's/8080/9090/g' /opt/apache-tomcat-11/conf/server.xml` |
| Deploy `.war` app | `sudo mv sample.war /opt/apache-tomcat-11/webapps/`                 |
| Logs              | `/opt/apache-tomcat-11/logs/catalina.out`                           |

---

## 💡 Notes / Tips

* Always download from the **bin/** directory — **not src/**.
* Use `startup.sh` and `shutdown.sh` to control Tomcat manually.
* If deployment fails, check `catalina.out` for error details.
* Tomcat’s **default web root** is `/opt/apache-tomcat-11/webapps`.
* Restart Tomcat after any `.war` deployment or port change.

---

## ✅ References

* [Apache Tomcat 11 Documentation](https://tomcat.apache.org/tomcat-11.0-doc/index.html)
* [Systemctl & Process Management Guide](https://www.freedesktop.org/software/systemd/man/systemctl.html)
* [Linux sed Command Manual](https://man7.org/linux/man-pages/man1/sed.1.html)
