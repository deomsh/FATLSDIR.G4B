## FATLSDIR.G4B v0.1 (20241001)

<pre><code>Functions: front-end for Grubutil 'FAT' function 'dir' or for 'ls'  
FATLSDIR.G4B [--mdbase=sector] [DEVICE][/PATH/][FILE] switches  
FATLSDIR.G4B /? (this text)  
DIR files on DEVICE. If DEVICE and/or PATH omitted: on ROOT  
DIR on hidden partitions too! *  
On FAT partitions: default 8+3 File Names (or use /lfn[:]case, see there)  
Arguments space-separated! Switches: lower/uppercase free  
--mdbase=sector changes (md)-startsector in use (default=0x3000) **  
DEVICE = (fd#), (hd#,#), (0x#) or (#); with ISO/UDF CD/DVD too  
/PATH/ = starting directory => without DEVICE => on root (PATH/ okay)  
/PATH/ accepts ONE wildcard: '*' at END of NAME[.EXT] in LAST directory  
FILE = DIR specified file => on root without DEVICE and/or /PATH/ 3*  
FILE accepts wildcard: '*' in END of Name & END of Extension (NOT: '?' )  
*  Default verbose DIR: DIR & output messages too  
** FAT-DIR parsing needs 0x1000 total memory (2MB) - LS-DIR 0x200 (512KB)  
** Lowest value 0x3000 - forbidden: 0x3001-0xD460 and 0x12000-0x12FFF  
3* FILE without DEVICE/PATH/ => before FILE no '/' allowed (FILE not /FILE!)  
3* Without FILE full directory will be shown (*.* is NOT needed)  

General switches: /s[:n] /o:d|f /b /w:[n] /p /q /[-]x:~ /[-]y:DIR  
/s[:n] = parse max 18 subdirectories deep: with /s:1-18 choice 1-18 levels  
/o:d|f = sort order: directories or files first  
/b = output filenames only - with /s DEVICE and PATH on each line too  
/w:[n] = output default in 5 columns - with /w:2-5 choice 2-5 columns *  
/p = pause after each screen, Q can be used to quit (partly: Grub4dos for Uefi)  
/q = quiet DIR: error messages & last file-count message only (not: /b or /w)  
/[-]x:~ = only SFN-equivalent of LFN/real shortened LFN will [not] be shown **  
/[-]y:DIR = only PATH [not]containing DIR parsed - accepts '*'-wildcard 3*  
*  Checks for graphicsmode 3/ 640x480 (80 chars on one screen-line needed)  
** Instead of '~' MAX 16 other characters can be used too (special feature)  
3* DIR is last directory in PATH - [-]DIR max 16 chars, later parts of PATH too  
3* Can be combined with '*' at end of last DIR in PATH to check chars after '*'  

FAT Directory Parser Switches: /a:[-]darsh /l /f /sfn[:]@ *  
/a:[-]d[-]a[-]r[-]s[-]h = [not] parse files/directories with attribute(s) **  
/l = all PATH & FILE output in /l => lowercase (default uppercase)  
/f = do not parse empty subdirectories  
/sfn[:]@ = show external saved LFN's for 'tilded' SFN-files/SFN-directories 3*  
*  Default - no DIR on NTFS, ISO-9660, UDF, EXFAT, EXT2/3/4 & ReIseR(2)fs  
*  If supported non-FAT file-system found: auto-switching to /ls-mode  
*  About max 36 000 files AND max 3 000 subdirectories in one directory  
** Attributes are not shown by FAT - only [not]parsed  
3* Long File Names saved by FATCOPY.G4B /sfn:@ (mixed-case SFN's not), no /b /w  

LS Directory Parser Switches: /lfn|/sfn /a:[-]d /l|u /f /$ /l+f *  
/lfn = ls-directory parsing: shows LFN on FAT, otherwise auto-switching **  
/sfn = shows LFN as-if SFN. Files max SFN~1000.EXT, directories max ~9 **  
/a:[-]d => /a:d show directories only, /a:-d files only. Can be used with /s  
/l|u = all PATH & FILE output in lowercase OR uppercase (/sfn auto uppercase)  
/f = do not parse empty subdirectories (NOT working on NTFS!)  
/$ = parse NTFS $-(meta)files/directories (default is skipped) 3*  
/l+f = parse directory lost+found on Ext2/3/4/ReIseR(2)fs etc. 3*  
*  About max 10 000 8+3 files/ subdirectories in one directory  
*  Parses FAT, NTFS, ISO-9660, UDF, EXFAT, Ext2/3/4 & ReIseR(2)fs etc.  
*  Case-sensitive in PATH/FILE and /[-]x: and /[-]y: with EXT2/3/4/ReIseR(2)fs  
** LFN in PATH/FILE with spaces between "quotes" or use escaped '\ ' ('\=' too)  
3* (Self-declared) Experts only! $-(meta)files can grow above 4GB  

Special Switches: /nocase /dirsize:n /maxfiles:N /maxbyte:n /size:n  
/nocase = set case-sensitive File Systems to case-insensitive  
/semicol = do not remove file-number suffixes, on ISO-9660 and UDF only  
/dirsize:N = max number of files parsed in each directory. Takes 'Nk' too  
/maxfiles:N = max total number of files parsed - takes 'Nk' & 'Nm' too  
/maxbyte:n = max total bytes parsed - takes 'nk' bytes and 'nm' bytes too  
/size:n = only files with filesize 'n' bytes showed - takes 'nk/nm' bytes too *  
*  /a:-d is auto-set (not working with: /a:[-]d[-]a[-]r[-]s[-]h and /a:[-]d)  

Remarks:  
Key 'Escape' can be used to interrupt parsing, with quit/ continue dialog (NOT on Grub4dos for UEFI)  
File versions: Grubutil FAT and Grub4Dos 0.4.6a, Grub4dos for UEFI (watch FAT!)  
Found not compatible with Grub4Dos 0.4.5b / Grub4Dos 0.4.5c / Grub4efi textmode  
FAT needed, searched in %^~dp0, (bd), ROOT: /, /boot/grub/, /grub/ and /g4dll/  
Grud4dos for UEFI soon 'out of malloc memory' (latest version 20240901)  
More convenient => insmod DEVICE/PATH/FATLSDIR.G4B DIR (watch loading FAT!)  
Based on copyFF.bat (:cpa & :copyfiles & :sub-dir => originator of call's seems to be Chenall)  

Example FATLSDIR.G4B  
Example FATLSDIR.G4B /b /s /p  
Example FATLSDIR.G4B /w /s  
Example FATLSDIR.G4B (hd0,0) /q  
Example FATLSDIR.G4B (fd0)/ /o:d /s  
Example FATLSDIR.G4B (hd0,0)/WINDOWS/*.EXE  
Example FATLSDIR.G4B (hd0,0)/WINDOWS/MS*.DLL /s  
Example FATLSDIR.G4B (hd0,0)/WINDOWS/SYS*/*.vxd  
Example FATLSDIR.G4B (hd0,0)/WINDOWS/ /-y:SYSTEM /s  
Example FATLSDIR.G4B (hd0,0)/PROGRA~1/ /s:2 /x:~  
Example FATLSDIR.G4B (hd2,4)/ /s /sfn:@  
Example FATLSDIR.G4B (hd0,0) /a:hr /s /f  
Example FATLSDIR.G4B (0xe0) /sfn /s  
Example FATLSDIR.G4B (hd2,0)/$* /$  
Example FATLSDIR.G4B (hd3,4)/lost+found/ /l+f /nocase /l  
Example FATLSDIR.G4B (0xe0) /semicol  
Example FATLSDIR.G4B (hd0,0)/Program\ Files/ /dirsize:4 /a:-d /s /f /lfn  
Example FATLSDIR.G4B "(hd0,0)/Program Files/" /maxfiles:2000 /s /lfn  
Example FATLSDIR.G4B (hd0,0) /maxbyte:64m /s  
Example FATLSDIR.G4B (hd0,0)/WINDOWS/ /size:0 /s /lfn</code></pre>    

### HISTORY
Version v0.1  
First published version

### SCREENSHOTS

FAT and ls directory parsing on ROOT (switch /lfn needed on fat only)

![FATLSDIR G4B use on root, with -s, and -s   -lfn on FAT12 I](https://github.com/user-attachments/assets/160f42c4-cb44-4c59-af7d-63b77bc3aff8)

Uses of switch /w (length of line 80 chars only - textmode or 640x480)

![FATLSDIR G4B use of wide (-w) and -s II](https://github.com/user-attachments/assets/4e020ff3-162b-4218-8377-b7fe00a1bbaa)

![FATLSDIR G4B use of wide (-w) and -s and -lfn III](https://github.com/user-attachments/assets/7fcb65d4-fb95-47ac-ae16-61cd253b0b34)

More advanced use of switch /s with /s:n (max directory depth is 18 directories)

![FATLSDIR G4B use of wide (-w) and -s=1 and -s=2 and -lfn IV](https://github.com/user-attachments/assets/2d151c06-2153-4735-a6f5-f1d5e1d757f6)

Use of switch /b (after Quit pager)

![FATLSDIR G4B use of list (-b) after Quit VI](https://github.com/user-attachments/assets/b0d87d5f-e5f8-4ab9-b593-04e03fdfae4c)

Use of switch /b with /s, /lfn and sort /o:d (after Quit pager)

![FATLSDIR G4B use of list (-b) and -s and -lfn afte Quit V](https://github.com/user-attachments/assets/88346d50-5e97-4b91-b55c-88367d852482)

Search and parse directories with switch /y:DIR

![FATLSDIR G4B search directories with switch -y=DIR with -w VII](https://github.com/user-attachments/assets/c32d6383-3c17-4297-bd84-13345a501ffa)

Search and parse directory including sub-directories with switch /y:DIR conmbined with /s

![FATLSDIR G4B search directories with switch -y=DIR with -s, -lfn and -b VIII](https://github.com/user-attachments/assets/db7b5e62-3ffa-47f9-9e6b-c919e0f85382)

Use of special switch /size:n

