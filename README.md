# PSRUTI
PSRUTI is a tool to tune midifiles of the standard formats SMF0 and SMF1 to be used at Yamaha XG/XF synthesizers, in particular keyboards. The program performs most of the standard functions of sequencers in a more easy way. All special features of Yamaha XG and XF are considered contrary to manufacturer independent software programs.

## Downloads and documentation

[Official PSRUTI Home Page](https://www.heikoplate.de/psruti.html)

## Development

PSRUTI is programmed with Visual C++ for Windows since Windows 98. The program applies the functions of my Opensource MIDI file library [HP MIDIFILE]( https://github.com/HeikoPlate/hpmidifile).

The further development has been stopped, but the tool has been published under the [MIT license](LICENSE) to make further improvements possible.

### Development hints in German

Erzeugung mit Visual C++ Version 6.0

#### 1. Verzeichnisse unter psruti_x-y

* hlp_eng         
Alles was für die Erstellung der engl. Dokumentation erforderlich ist
* hlp_germ        
Alles was für die Erstellung der deutschen Dokumentation erforderlich ist
* Lieferstand     
Dateien, die für die Auslieferung benutzt werden
* NSI-Installation        
Quelldatei .nsi und .exe des Installationsprogramms
* psruti_res_eng  
Resourcen-Projekt zur Erstellung der engl. Resourcen DLL
* psruti_res_germ 
Resourcen-Projekt zur Erstellung der deutschen Resourcen DLL
* Debug, Release  
C++ Objektverzeichnisse für psruti.exe
* res             
Bild-Dateien

#### 2. HP_MIDIFILE

Unter Projekt, Einstellungen, Linker muss die Bibliothek HP_midifile.lib 
eingetragen sein. Diesen Modul wird ins Projektverzeichnis  
sowie nach Debug und Release kopiert.

PSRUTI benötigt zum Start den Modul HP_midifile.dll in den Programmverzeichnissen, muss also mit ausgeliefert werden; d.h. nach Lieferstand kopieren.

#### 3. Mehrsprachige Dokumentation aus odt-Files erzeugte PDF Files (Verzeichnisse hlp_eng, hlp_germ)
Die PDF-Files werden unter den Namen

psrutixy_germ.pdf (Manual)
psruti_germ.pdf (Hilfe: identischer Inhalt)

psrutixy_eng.pdf (Manual)
psruti_eng.pdf (Hilfe: identischer Inhalt)

in den Ordner Lieferstand kopiert. Die Manuals werden gesondert ausgeliefert.

#### 4. Mehrsprachige Resourcen (Verzeichnisse psruti_res_eng, psruti_res_germ)

Vorgehensweise bei der Entwicklung (nur bei Änderung der Resourcen)

a) In der PSRUTI-Quelldatei psruti.cpp wird das define

```
   #define WITH_DLL_RESOURCES
```

   zur Deaktivierung der Language-Resource-dll's in Kommentar gesetzt. Damit wird die lokal beim Programm befindliche deutschsprachige Resource psruti.rc verwendet, die man jetzt unter C++ anpasst.

b) Wenn fertig, die resource.h und psruti.rc in den zur Sprache "Deutsch" gehörende Ordner psruti_res_germ kopieren, die rc-Datei in psruti_res_germ.rc umbenennen (alte löschen) und mit C++ in diesem Verzeichnis die Release-Fassung psruti_res_germ.dll erzeugen.
   
c) In dem anderen Verzeichnis psruti_res_eng die Datei resource.h übernehmen. In psruti_res_eng.rc vor Erzeugung der dll die in der deutschen Fassung geänderten sprachspezifischen Einträge durch entsprechende englische ersetzen. Release-Fassung psruti_res_eng.dll 

Hinweis: Bei der Erstellung beider Resourcen gibt es drei Warnungen, die aber nichts bedeuten.    
   
d) Beide dll gehören in die Programm-Verzeichnisse Debug, Release und nach Lieferstand.

e) Zum Abschluss den Kommentar gemäß a) entfernen und Sprachumschaltung testen.

#### 5. Erstellung der Setup-Datei mit NSIS (Verzeichnis NSI-Installation)

   Die Datei psrutixy.nsi mit Texteditor bearbeiten.
   
   Nur die oberen Zeilen müssen angepasst werden:
```   
   ==========================
   #T01.01.2013
   #A01
   ##{{NSIS_PLUS_END_TODO}}##
   
   !define PROJECT         "PSRUTIxy"
   !define FLATPROJECT     "psrutixy"
   !define NAME            "PSRUTI"
   !define VER_MAJOR               x
   !define VER_MINOR               y
   !define ICON_NAME       "PSRUTI"
   !define PATH            "C:\Programmierung\psruti_x-y\Lieferstand\"
   !define OUTF            "${FLATPROJECT}_setup.exe"
   ==========================
```

Für die Erzeugung der psrutixy_setup.exe müssen in "Lieferstand" folgende aktuelle Dateien vorliegen         
   
* HP_midifile.dll
* psruti.exe (Release-Version)
* psruti_eng.pdf
* psruti_germ.pdf
* psruti_res_germ.dll
* psruti_res_eng.dll

Dann nsi-Datei kompilieren (Rechte Maustaste; "Compile NSI Script"). Es entsteht eine Datei psrutixy_setup.exe, die nach Lieferstand kopiert wird.
   
6. Erstellung der Datei psrutixy.zip im Verzeichnis Lieferstand
 
   psrutixy.zip bekommt nur die psrutixy_setup.exe.
   
7. Zum Abschluss die vollständige Installation, Lauf und Deinstallation testen. 

8. Dynamischer Test mit Logfile.

   In StdAfx.h muss das Define HP_LOG aktiviert werden (Kommentar entfernen).

   An den geeigneteten Programmstellen muss (hpmfi->lf)->add(format, par1, par2...) eingetragen werden.

   Mehr ist nicht zu tun. Das Logfile "psruti_log.txt" wird im Ordner Dokumente abgelegt.    

9. Debugging unter Vista

   Visual C++(6.0) CFileDialog DoModal() does not work with Debugging under Vista
   For debugging a midifile define DEBUG_SOURCE in psruti_dlg.cpp with a source path
   These lines are predefined in this file. Delete or insert the comment //.
