# RentCarProject

## Car Rental System

**Terminal-based Car Rental Application** developed using **Java 21**, **PostgreSQL**, **JDBC**, and **Maven**.  
The project applies **Clean Architecture**, **OOP**, **SOLID principles**, and **Dependency Inversion** to ensure modular, maintainable, and scalable code.

---

## Features

- **User Management & Authorization**
  - Roles: `ADMIN` and `CUSTOMER`
  - Login/Logout with **Singleton Session Management**
  - Passwords hashed with SHA-256
- **Vehicle Management**
  - Add, update, delete, and list vehicles (Admin)
  - Vehicle types: Car, Helicopter, Motorcycle
  - Hourly, daily, weekly, and monthly pricing
- **Rental System**
  - Booking, cancellation, and availability checks
  - Deposit calculation and lifecycle management
  - Age and vehicle value restrictions for certain rentals
- **Search & Filter**
  - Filter by type, brand, and price range
  - Pagination support
- **Error Handling**
  - Proper exception handling for expected and unexpected errors
  - User-friendly console messages
- **Transaction Management**
  - All rental operations handled atomically using transactions

---

## Technologies & Architecture

- **Language:** Java 21
- **Database:** PostgreSQL
- **Database Access:** JDBC
- **Build & Dependency Management:** Maven
- **Architecture:** Clean Architecture, Layered Design
- **Principles:** OOP, SOLID, Dependency Inversion
- **Packaging:** Executable JAR

---

## Database Schema

[DatabaseReadMe.md](readmeFiles/DatabaseReadMe.md)

---

## Package Structure

[PackageStructureReadMe.md](readmeFiles/PackageStructureReadMe.md)

---

## UI

[SignUpAndLogin.md](readmeFiles/UI/SignUpAndLoginUI.md)

[AdminUI.md](readmeFiles/UI/AdminUI.md)

[CustomerUI.md](readmeFiles/UI/CustomerUI.md)

---

# Code Review

<a href="https://youtu.be/r1xC8by2EFw">Code Review's Video</a>

---
## Installation & Running

<a href="https://www.youtube.com/playlist?list=PLZ01JzwQ4HSx6cQJzp5dCwEVzEqwF5MRG"> Project Setup Playlist</a>

---

## Database Setup

This project uses PostgreSQL 17.6. You can use the database backup file provided in this repository.  
Follow the steps below to install PostgreSQL and restore the backup.

### Installing PostgreSQL 17.6

- **macOS (Homebrew)**
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```bash
brew install postgresql@17
```
```bash
brew services start postgresql@17
```
```bash
brew install psql
```

- **linux** 
```bash 
sudo apt update
```
```bash 
sudo apt install postgresql-17
```
```bash 
sudo systemctl start postgresql
```

- **windows**
  Download the installer from <a href = "https://www.postgresql.org/download/windows/?utm_source=chatgpt.com" > PostgreSQL official site </a> and follow the instructions.
  Make sure the PostgreSQL service is running after installation.

---

### Restoring the Backup
1. Download <a href="https://github.com/AliBiner/Rent-a-Car/blob/main/db.sql"> DB Backup </a>
2. Open terminal/command prompt.
3. Run the following command to restore the database from backup.
4. If you do not have superuser:

**macOS (Homebrew)**
- Open psql on the terminal
```bash
psql postgres
```
- Create superuser
```bash
CREATE USER <username> WITH PASSWORD 'any passwords';
```
- And Press Enter
- If creating success, close the terminal


**windows**
```bash  
# Windows (Command Prompt)
psql -U <your_postgres_user> -d <your_db_name> -f C:\path\to\backup.sql
```

Replace <your_postgres_user> and <your_db_name> with your PostgreSQL username and database name. 
After this, the database is ready to use with the application.

---

## Installing Java JDK 21

This project requires **Java 21** to compile and run.  
Below are instructions for installing JDK 21 on different operating systems.

### macOS

**Option A: Homebrew**
- Update Brew
```bash
brew update
```
- Install JDK 21
```bash
brew install openjdk@21
```
- Add JDK 21 to PATH
```bash
echo 'export PATH="/usr/local/opt/openjdk@21/bin:$PATH"' >> ~/.zshrc
```
```bash
source ~/.zshrc
```

- Verify installation
```bash
java -version
```

**Option B: Official Oracle JDK**
1. Download JDK 21 from Oracle Downloads
2. Install the .dmg file.
3. Verify installation:
```bash 
  java -version
```

### Linux(Ubuntu/Debian)

**Option A: Using apt repository**
```bash
sudo apt update
sudo apt install openjdk-21-jdk

# Verify installation
java -version
```
**Option B: Download from Oracle**
1. Download JDK 21 from Oracle Downloads
2. Download .tar.gz archive.
3. Extract and set JAVA_HOME:
```bash 
tar -xzf jdk-21_linux-x64_bin.tar.gz
sudo mv jdk-21 /opt/

# Add to PATH
echo 'export JAVA_HOME=/opt/jdk-21' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# Verify
java -version
```

### Windows
1. Download the JDK 21 installer from Oracle JDK 21 Downloads
2. Run the .exe installer and follow the instructions.
3. Set JAVA_HOME environment variable:
   - Open System Properties → Environment Variables → New System Variable
   - Name: JAVA_HOME
   - Value: path to JDK 21 folder, e.g., C:\Program Files\Java\jdk-21
4. Add %JAVA_HOME%\bin to your PATH variable.
5. Verify installation:
```bash
java -version
javac -version
```

---

## Running the Application (JAR + Command Line Arguments)

After building the project with Maven, you will get a `.jar` file.  
This application requires **four command-line arguments** to run:

1. `DB_URL` – JDBC URL of your PostgreSQL database (required)
2. `DB_USER` – Database username (required)
3. `DB_PASSWORD` – Database password (required, can be empty)
4. `TEST_MODE` - Open Test Options (required, can be empty)

### Example Usage

#### macOS / Linux
```bash
java -jar presentation-1.0-SNAPSHOT.jar "jdbc:postgresql://localhost:5432/mydb" "myuser" "mypassword" "test"
# Or with an empty DB_PASSWORD  and an empty TEST_MODE
java -jar presentation-1.0-SNAPSHOT.jar "jdbc:postgresql://localhost:5432/mydb" "myuser" "" ""
```
#### Windows (Command Prompt / PowerShell)
```bash
java -jar presentation-1.0-SNAPSHOT.jar "jdbc:postgresql://localhost:5432/mydb" "myuser" "mypassword" "test"
# Or with an empty DB_PASSWORD and an empty TEST_MODE
java -jar presentation-1.0-SNAPSHOT.jar "jdbc:postgresql://localhost:5432/mydb" "myuser" "" ""
```
### Notes:
- All four arguments are required.
- TEST_MODE and DB_PASSWORD can be empty, but DB_URL and DB_USER cannot be empty.
- The application reads these arguments at startup and connects to the PostgreSQL database.
