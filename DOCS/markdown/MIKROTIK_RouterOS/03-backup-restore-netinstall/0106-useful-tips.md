## Useful tips 

Useful snippet to clean up the BASH script from Windows formatting that may interfere with the script if it's edited on a Windows workstation: 

```
sed -i -e 's/\r$//' *.sh
```

139
