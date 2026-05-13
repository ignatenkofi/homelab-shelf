## Running function from another function 

Same as above applies also to functions. If you want to run function from another function then it need to be declared. 

```
:global test do={
 :return ($1 + 1)
}
:global testtest do={
 :local x 5
 :local y [$test $x]
 :put "typeof = $[:typeof $y]"
 :put "testets_res=$y"
}
```

Code above will not work as expected, output will be: 

```
typeof = nil
testets_res=
```

To fix this we need to declare global "test" in "testtest" function 

1126 

```
:global testtest do={
 :global test
 :local x 5
 :local y [$test $x]
 :put "typeof = $[:typeof $y]"
 :put "testets_res=$y"
}
```
