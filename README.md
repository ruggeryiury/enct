<div align=center>
<img src='https://raw.githubusercontent.com/ruggeryiury/enct/main/assets/header.webp' alt='ENCT: Package Header Image'>
</div>

<div align=center>
<img src='https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/csharp/csharp-original.svg' width='48px' title='JavaScript'/>
</div>

<div align=center>
<img src='https://img.shields.io/github/last-commit/ruggeryiury/enct?color=%23DDD&style=for-the-badge' /> <img src='https://img.shields.io/github/repo-size/ruggeryiury/enct?style=for-the-badge' /> <img src='https://img.shields.io/github/issues/ruggeryiury/enct?style=for-the-badge' /> <img src='https://img.shields.io/github/package-json/v/ruggeryiury/enct?style=for-the-badge' /> <img src='https://img.shields.io/github/license/ruggeryiury/enct?style=for-the-badge' />
</div>

ENCT files (**Enc**rypted **T**ext file) has a file extension of `.enct` and it's used to store sensitive data using AES encryption.

## File header

An ENCT file has a fixed header of `0x50` bytes length.


| NAME                  	| OFFSET 	| LENGTH 	| TYPE                  	| DESCRIPTION             	|
|-----------------------	|--------	|--------	|-----------------------	|-------------------------	|
| Magic                 	| `0x0`  	| `0x4`  	| ASCII `string`        	| Magic "ENCT"            	|
| FileVersion           	| `0x4`  	| `0x2`  	| Unsigned 16-bit `int` 	| File version            	|
| CreationDate          	| `0x6`  	| `0xA`  	| ASCII `string`        	| File creation date      	|
| CreationTime          	| `0x10` 	| `0x8`  	| ASCII `string`        	| File creation time      	|
| SourceFileContentSize 	| `0x18` 	| `0x4`  	| Unsigned 32-bit `int` 	| File content size       	|
| SourceFileType        	| `0x1C` 	| `0x2`  	| Unsigned 16-bit `int` 	| Source file type        	|
| Padding               	| `0x1E` 	| `0x2`  	| `byte[]`              	| File header padding     	|
| IV                    	| `0x20` 	| `0x10` 	| `byte[]`              	| IV                      	|
| SrcFileHash           	| `0x30` 	| `0x20` 	| `byte[]`              	| Source file SHA256 hash 	|

- `Magic`: The file header magic (an ID identifier of the file) as an ASCII-encoded `string` of 4-bytes length. All ENCT files has the same 4-byte.

- `FileVersion`: The file version as an unsigned 16-bit integer, used to track down the version of the file itself. With this, ENCT is able to switch to new methods of creation/decryption for each file version dynamically.

- `CreationDate`: The file creation date as an ASCII-encoded `string`.

- `CreationTime`: The file creation time as an ASCII-encoded `string`.

- `SourceFileContentSize`: The source file content size.

- `SourceFileType`: The source file type as a `byte`. Known values are:
  - `0x0` - `.txt` file.
  - `0x1` - `.json` file.

- `Padding`: An empty bytes padding of 2-bytes.

- `IV`: The **i**nitialization **v**ector used on the file encryption. Each 2-bytes are swapped.

- `SrcFileHash`: A computed SHA256 hash of the source file.