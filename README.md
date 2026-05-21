# SNOMED CT Database Creation and Import Tool (Swiss Edition)

This Java project creates a MySQL database and imports SNOMED CT data, including both the International Edition and the Swiss Extension (CH Edition), using the Full release format.

## Features

- Creates a MySQL database
- Creates all required tables for SNOMED CT Full release:
  - `full_concept`
  - `full_description`
  - `full_relationship`
  - `full_refset_Simple`
  - `full_refset_ExtendedMap`
  - `full_refset_Language`
  - `full_refset_ModuleDependency`
- Imports SNOMED CT International Edition Full release files
- Imports Swiss Extension Full release files (German, French, Italian, English)
- Adds indexes to improve query performance

## Requirements

- Java 8 or higher
- MySQL 8.x
- MySQL Connector/J (JDBC driver)
- SNOMED CT Full release files (download here: https://mlds.ihtsdotools.org/ (registration required):
  - **International Edition**
  - **Swiss Extension**

## Configuration

### 1. Update paths and release identifiers

Open `CreateDatabaseAndImportData.java` and set the following variables to match your environment:

```java
static String ReleaseFilePath = "PATH_TO_YOUR_INTERNATIONAL_EDITION";
static String ReleaseFilePathCH = "PATH_TO_YOUR_SWISS_EXTENSION";
static String ReleaseDate = "20250101"; // International Edition release date
static String ReleaseDateCH = "CH1000195_20241207"; // Swiss Extension release identifier

### 2. Database credentials

Set your local MySQL credentials and connection parameters:
```bash
String dbUser = "root";
String dbPassword = "";
String dbURL = "jdbc:mysql://localhost/";
```

Make sure `allowLoadLocalInfile=true` and `allowMultiQueries=true` are enabled in your connection string.

### 3. File structure expected

The tool expects SNOMED CT files to follow the official Full release folder structure, e.g.:
```bash
International Edition/
└── Full/
    └── Terminology/
        ├── sct2_Concept_Full_INT_20250101.txt
        ├── sct2_Description_Full-en_INT_20250101.txt
        └── sct2_Relationship_Full_INT_20250101.txt
    └── Refset/
        └── Language/
            └── der2_cRefset_LanguageFull-en_INT_20250101.txt

Swiss Extension/
└── Full/
    └── Terminology/
        ├── sct2_Concept_Full_CH1000195_20241207.txt
        ├── sct2_Description_Full-de-ch_CH1000195_20241207.txt
        ├── sct2_Description_Full-fr-ch_CH1000195_20241207.txt
        ├── sct2_Description_Full-it-ch_CH1000195_20241207.txt
        ├── sct2_Description_Full-en_CH1000195_20241207.txt
        └── sct2_Relationship_Full_CH1000195_20241207.txt
    └── Refset/
        └── Language/
            ├── der2_cRefset_LanguageFull-de-ch_CH1000195_20241207.txt
            ├── der2_cRefset_LanguageFull-fr-ch_CH1000195_20241207.txt
            ├── der2_cRefset_LanguageFull-it-ch_CH1000195_20241207.txt
            └── der2_cRefset_LanguageFull-en_CH1000195_20241207.txt
```
**Note:** Some optional imports (e.g., simple refsets, extended maps) are commented out in the code and can be enabled as needed.


## How to Run (Eclipse IDE)
To run this project using Eclipse:

1. **Import the project into Eclipse**
   - Open Eclipse.
   - Go to `File` > `Import...` > `General` > `Existing Projects into Workspace` > `Next`.
   - Browse to the folder containing this project.
   - Click `Finish`.
     

2. **Edit the configuration if needed**
   - In the class `CreateDatabaseAndImportData.java`, update the following variables to match your system:
     ```java
     static String ReleaseFilePath = "C:\\Path\\To\\InternationalEdition";
     static String ReleaseFilePathCH = "C:\\Path\\To\\SwissExtension";
     static String ReleaseDate = "20250101";
     static String ReleaseDateCH = "CH1000195_20241207";
     ```

3. **Run the program**
   - Right-click the class `CreateDatabaseAndImportData.java`.
   - Select `Run As` > `Java Application`.

4. **Verify the result**
   - The MySQL database `SCT:CH_Dec24` should now be created.
   - Tables will be created and populated with SNOMED CT data.
   - The Eclipse console will show logs confirming successful steps.

> **Note:** Ensure that:
> - MySQL is running locally.
> - The user has privileges to create/drop databases.
> - `LOAD DATA LOCAL INFILE` is enabled in both MySQL server configuration and JDBC driver.

## Acknowledgments
[SNOMED International](https://www.snomed.org/)
