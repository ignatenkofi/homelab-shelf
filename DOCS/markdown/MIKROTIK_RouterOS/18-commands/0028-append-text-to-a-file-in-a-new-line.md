## Append text to a file in a new line 

There is no direct way to append text to a file, however you can store the old content and append to it in a new line: 

```
:local oldText [/file get test.txt contents as-string]
:local addText "test append"
:local newText ($oldText."\n".$addText)
/file set myFile.txt contents=$newText
```
