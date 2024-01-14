# file-organization-kitless

## Introduction

Personal small utilities I made while organizing file backups, such as filename and minor file content modifications, file/folder hash logging.

As the title suggests, this is not an all-powerful toolbox, and may not achieve the effects you expect. It's best understood as a wrench or an X-acto knife.

Please feel free to correct me if there are any ambiguities or unprofessional wording.

## Categories

A script name consists of tags and descriptions, e.g. "Nlr-Fd/Delete files with duplicate filename elements by length". Tags are ordered by execution sequence. The initial tags are named by action, object and type, e.g. "eNlr-aFd/Delete...". I felt this was redundant so I removed the action indicator. Tags cannot fully represent implemented functions, but can serve as an index, although there are not many. Here are the letter meanings:

| N               |                |                        |         |                    |
| --------------- | -------------- | ---------------------- | ------- | ------------------ |
| Filename        |                |                        |         |                    |
| I               | d              | r                      |         |                    |
| Insert          | Delete         | Replace                |         |                    |
| *e*             | *l*            | *r*                    |         |                    |
| *Limit element* | *Limit length* | *Repeat*               |         |                    |
| **F**           |                |                        |         |                    |
| File            |                |                        |         |                    |
| c               | d              | m                      | r       |                    |
| Create          | Delete         | Write/Delete (content) | Replace |                    |
| **P**           |                |                        |         |                    |
| Path            |                |                        |         |                    |
| *n*             | *p*            | m                      | s       | *t*                |
| *Nested*        | *Path*         | Merge                  | Split   | *Transfer element* |

## Usage

Usage is included in the comments at the beginning of each file. I've replicated them here. The last line of each section shows expected outcomes.

##### Fe-Fcm/Generate a folder (file) hash log

Specify folder to operate on: For Mac as example, to operate on files in Downloads/r24 folder, set folder variable in line 16 as 'Users/your_username/Downloads/r24'

Use SHA1 algorithm by default. To change to MD5, SHA256, SHA512 etc, replace sha1 in line 29 with your desired algorithm name in lowercase

Default log file name format is original_filename+'_hash.log'. To modify the file name format or suffix, change '{folder}_hash.log' in line 18. For example, to change file name format to original_filename+'-shha.log', set it to: logging.basicConfig(filename=f'{folder}-shha.log', level=logging.INFO)

Default log format is INFO:root:hash_generation_time - original_file_path - file_hash_value. To change the format, modify line 38 (f'{time_now} - {folder} - {folder_hash}'). For example, to change log format to path: original_file_path hash: file_hash_value, set it to: logging.info(f'path: {folder} hash: {folder_hash}')

Default time format is year-month-day-hour-minute-second-millisecond-microsecond. To change it, modify the strftime format string in line 37 '%Y-%m-%d-%H-%M-%S-%f'. For example, to change time format to month-day-year hour:minute:second, set it to: time_now = datetime.datetime.now().strftime('%m-%d-%Y %H:%M:%S')

Expected outcome: After first run, r24_hash.log will be created in Downloads, containing info like hash value, path for each file. Subsequent runs will append to the log with the same format.

##### Ne-Nr/Replace specific characters in filenames

Specify character to be replaced: To replace '_ ', set replace_this variable in line 10 as '_ ' 

Specify replacement character: To replace with '-', set replace_with variable in line 11 as '-'

Filename '2021_ 10_ 01.jpeg' becomes '2021- 10- 01.jpeg'

This can also be fully achieved via GUI: https://support.apple.com/en-gb/guide/mac-help/mchlp1144/mac

##### Nel-Na/Skip filename characters from specific direction and insert specified string

Specify string to insert: To insert '-', set insert_str variable on line 15 as '-'

Specify insert direction: 'front' for forward direction, 'back' for backward  

Specify number of characters to skip: If length is 2, set skip_length variable on line 17 to 1

If original filenames are '1234.png' and '5678.jpg', with insert_str = '-', insert_direction = 'front', final names will be '1-234.png' and '5-678.jpg'. If insert_direction is backward, final names will be '123-4.png' and '567-8.jpg'

Partially achievable via GUI: https://support.apple.com/en-gb/guide/mac-help/mchlp1144/mac

##### Nl-Fd/Delete files with duplicate filename elements by length

Define length of duplicate element: If duplicate element is 3 characters, set duplicate_length variable on line 11 as 3 

Given files '0010.png', '1000.jpg', '0100.md', only '0010.png' will remain

##### Nl-Nd/Keep only a number of characters from filenames by direction

Specify number of characters to keep: To keep 2 characters, set keep_length variable on line 13 to 2

Specify keep direction: Set to 'front' for forward direction, 'back' for backward direction on line 14 with keep_direction variable 

If original filenames are '1234.png' and '5678.jpg', with keep_length = 2 and keep_direction = 'front', final names will be '12.png' and '56.jpg'. If keep_direction is set to backward, final names will be '34.png' and '78.jpg'

##### Nl-Nd/Skip and remove filename characters by length and direction

Specify number of characters to skip: To skip 2 characters, set skip_length variable on line 15 to 2

Specify number of characters to remove: To remove 1 character, set remove_length variable on line 16 to 1  

Specify remove direction: Set to 'front' for forward direction, 'back' for backward on line 17 with remove_direction variable

If original filenames are '1234.png' and '5678.jpg', with skip_length = 2, remove_length = 1, remove_direction = 'front', final names will be '124.png' and '568.jpg'. If remove_direction is backward, final names will be '134.png' and '578.jpg'

Partially achievable via GUI: https://support.apple.com/en-gb/guide/mac-help/mchlp1144/mac 

## Special

These are common needs, keywords should return similar solutions. I've considered file splitting/merging/XOR and improving other NF functions, but the (for me) massive engineering effort and lack of personal need to do so has prevented that. 

Indeed, "suite" is an overstatement - I will revise the name.

## License

```
MIT License

Copyright (c) [year] [fullname]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
