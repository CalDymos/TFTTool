# TFTTool: Parse and Convert TFT Files.

## Description

TFTTool is a python script that reads the TFT file and converts it into a human readable format (nicely formatted JSON). It also allows you to change the device model to a compatible one (same resolution, same series). This includes conversions of a Nextion file to a TJC file and vice-versa.

## Requirements

Python 3.7 or higher

## Usage

Get all details about the CLI by executing `python TFTTool.py -h`.

To simply convert a TFT file into a text file, use 

```
python TFTTool.py -i TFT_SOURCE -o TEXT_FILE
```

To change the device model, use 

```
python TFTTool.py -i TFT_SOURCE -t NEW_MODEL
```

Notes:
* Only a few models are currently supported for device model changes. If you want to help to increase the number of supported devices, create *any* TFT file for that device, and provide me the model and header 2 XOR key (that are the first lines of the text generated by this tool; you can't miss them!). Alternatively you can manually copy them from the file itself using a hex editor. The key is located at offset `0x3c-0x3f` (4 bytes).
* The text output contains a couple keywords:
	* `op:0x1234`: 0x1234 is an encoded operator that has not yet been decoded and added to the TFTParser source. Known operators get replaced by the right instruction from the Nextion Instruction Set.
	* `local:0x1234`, `global:0x1234`: 0x1234 is the address of a local/global variable.
	* `system:0x1234`: 0x1234 is the address of a system variable that has not yet been decoded and added to the TFTParser source. Known system variables get replaced by the right name from the Nextion Instruction Set.
	* `RAW_DATA`: This block seems to contain no recognized data. Therefore its represented as hex.

## Example

In the [Example](./Example) subfolder you'll find a [TFT file](./Example/HSV%20Test.tft) and the [resulting text file](./Example/HSV%20Test.txt). 

The HMI source file (and its license) can be found in this repository: https://github.com/MMMZZZZ/Random-Stuff/tree/eea7398335ff6a92c16227dbe911bf3e18e9728d/Nextion%20HSV%20Test