# SonicMEMS_PCB_SQL_Database Steps
1. Go to https://letos.org/ and download SQLite (now called LetOS)
2. Check that you have the proper SQLite3 drivers installed
   2a. Hit "Windows key" + "r" to pull up run command
   2b. Type "ODBCAD32.EXE" without ""
   2c. Go to "System DSN" tab. If there is no SQLite3 Datasource then perform step 3

# Installing SQLite 3 drivers
1. Goto http://www.ch-werner.de/sqliteodbc/ and download proper version. Make sure you use _w64 for 64bit systems.
2. Dont install SQlite 2 drivers during install when prompted.
3. Validate with step 2

# Setting up KiCAD
1. Install KiCAD.
2. Create a folder where all KiCAD files will be stored. For example, mine is "C:\Users\Luis\Desktop\KiCAD\"
3. Download the Database folder from this repository and place it inside the KiCAD folder. This is where all the setup files will be stored. For example, my full path would be "C:\Users\Luis\Desktop\KiCAD\Database"
4. Boot up KiCAD
5. On the main page select Preferences->Configure Paths
   5a. On this window add a path called "KICAD10_MAIN_DIR" with Path pointing to where you stored the KiCAD folder
   5b. Define another Path called "KICAD10_3DMODEL_DIR" with path pointing to ./Database/4_3DStep
   5b. Close KiCAD directly after and reopen
7. On the main window go to Preferences->Manage Symbol Libraries
   6a. Add a global library with the "+" button.
   nickname="SonicMEMS Database"
   library path="${KICAD10_MAIN_DIR}/Database/1_Database_Library/DB_Test.kicad_dbl"
   Library format="Database"
   
   6b. Add another global library with the "+" button.
   nickname="Resistors"
   library path="${KICAD10_MAIN_DIR}/Database/2_symbols/Resistors.kicad_sym"
   Library format="KiCad"

   6c. Continue step 6b for every file within the "2_sybmols" Folder

8. Exit out of the manage symbol library and go to main window
9. On the main window go to Preferences->Manage Footprint Libraries.
   8a. Add a global library with the "+" button.
   nickname="Capacitors"
   library path="${KICAD10_MAIN_DIR}/Database/1_Database_Library/Capactiors.kicad_dbl"
   Library format="KiCad"

   8b. Continue step 8b for every folder name within the "3_footprints" Folder.

10. All done! As long as you do not wish to add any components/symbols/footprints

# Adding component to database assuming reused symbol/footprint
1. If you want add a component while reusing a symbol and footprint then thats easy!
   1a. Example: This is if you wanted to add a new flavor 0603 resistor to the database (we have the footprint/symbol already made)
2. Navigate to where you saved TestDatabase.sqlite. Should be in ${KICAD10_MAIN_DIR}/Database/1_Database_Library/
3. Open TestDatabase.sqlite with SQLiteStudio
4. Open the Table corresponding to which device you are wanting to add. i.e: resisitor, inductor, etc..
5. Go to the "Data" tab and hit the green "+" to add a entry
6. Enter all the information you can. If you cant fill in then enter "-".
   6a. For entering the symbol use "Symbol library name":"symbol name"
     6a1. For example a typical resistor would use "Resistors:R"
     6a2. You can find all names within the KiCAD symbol editor
   6b. Repeat steps 6a but for the Footprint category as well.
7. Once finished then just hit the green checkmark button.
8. It will automatically update KiCAD and you should see it almost instantly update.

# Adding component to database assuming new symbol/footprint
1. This is for when you wish to add a componnet but do not have the symbol or footprint ready
   1a. Example: This is like if we wanted to add a IC but did not readily have its package/symbol already
2. Open Kicad and go to the symbol editor.
   2a. Draw a symbol with detail to the best of your ability. Try to avoid using empty boxes if possible unless the device is simple
   2b. Make sure to map the pins exactly to how the footprint would look.
   2c. Grab the name of the symbol and that will be used when inside of SQLite
3. Go the the footprint editor
   3a. Likely you can just download the footprint for online and upload it here instead of making your own.
   3b. Grab the name of the footprint and that will be used when inside of SQLite
4. Open SQLite and perform the earlier section but with the names for the Symbol and Footprint columns

# Adding 3D Model (REQUIRED IF ADDING FOOTPRINT)
1. If you addded a footprint then you must also include a 3D model. This is simple.
2. Grab the 3D model you downloaded and place it into ${KICAD10_MAIN_DIR}/Database/4_3DStep/
3. Open the footprint in Footprint editor and click "Footprint Properties"
   3a. Once open, go to the 3D Model tab.
   3b. IMPORTANT!: Enter the path to the 3D model but you must use the ${KICAD10_3DMODEL_DIR} variale when defining the full path. If you do not use this then it will not work for everyone else.
   3c. Adjust the 3D model scale/offset as needed.
4. Hit OK and all done!
