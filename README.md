#golangcheatsheet #golang
### Golang notes

I toke these notes while I was studying go from [Building web applications with Golang](https://astaxie.gitbooks.io/build-web-application-with-golang/content/en/)

1. Go uses UTF-8 character set.

2. There are 3 ways to define a variable.

3. booleans default value is false

4. Numerical types in go `rune, int8, int 16, int32, int64, byte, uint8, uint16, uint 32, uint64`.

5. go also support complex numbers `complex128, complex64` e.g `var c complex64 = 5+5i`

6. `float32, float64` are the types of float variables. there is no simple float in go 

7. `rune` is a alias of `int32` and `byte` is alias of `uint8`

8. `:=` kind of short hand definition can't be defined globally or outside of a function

9. unused variable will give you a compilation error

10. Strings can be represented by double quotes `""` or backticks `\``\` for multi-line strings.

11. Use group form definition to define multiple variables/constants. e.g `const (*vars)`

12. the group definition uses the last expression if the current item has no expression or assignment.

13. `iota` keyword is an `enumerator(0,1,2...)` can be used in group definition, it resets when it meets a new `const`

14. any variable that begins with Capital letter will be exported. There are no public/private keywords in Go

15. arrays can be defined as `var arrname [n]typeOfArry = {values sep by comma}`

16. arrays can't be passed as reference to other functions, where `slice` can

17. `a := [...]int{3,6,0}`, using `...` will make go define the length by it's self

18. multidimensional arrays can be defined as `doubleArray := [2][4]int{[4]int{1, 2, 3, 4}, [4]int{5, 6, 7, 8}}`

19. dynamic arrays are called `slice` in go

20. `slice` is not really a `dynamic array`. It's a reference type. `slice` points to an underlying `array` whose declaration is similar to `array`, but doesn't need length. `slice := []byte {'a', 'b', 'c', 'd'}` is how you define a slice.

21. `slice` is a reference type, if a function appends new item to the slice coming from outside and the slice don't have enough space due to which new slice will be created then the old slice will not change.

22. `slice` is a `struct` which contains 3 parts
    
    1. `pointer` where `slice` starts
    2. `length` of the `slice`
    3. `capacity`, the length from start index to end index
    
23. built-in `slice` functions
    1. `len` length of the slice, how many items it has
    2. `cap` capacity of the slice, now much items can it hold totally
    3. `append` appends items to the slice and returns a slice. Note append will change the array that slice is pointing to and affect the other slices that are point to the same array/slice. If there is not enough capacity in slice then append will create a new slice and return that new slice where the pointers which are pointing to the old slice won't be affected.
    4. `copy` copies items from one slice to another and returns the number of items that were copied
    
24. `map` behaves like `python` dictionary and can be defined as `var dict map[keytype]valuetype` or `dict := make(map[keytype]valuetype) {key:value,...}`. Map is a referenced type

25. it's impossible to print the map in a order every time it will be printed in a new way.

26. `len` works for map as well, there is no fixed length for map`delete(mapName, "key")` deletes the key/value pair from map

27. `make(Type, args)` allocates memory for built-in models like map, slice, channel and returns `Type` with the initial value/values assigned.

28. `new(Type)` allocates memory for the `Type` and returns a pointer to that memory.

29. there are 3 types of conditional statements in Golang, conditional, cycle control and unconditional jump

30. `goto` keyword reroutes to a previously defined variable with in the same code block.

31. `fallthrough` is used in `swtich` where the execution will fall through current case.

32. `select` and `swtich` are similar, In `select` each case waits for send/receive operation from a channel.

33. for loop can iterate over map, eg `for k,v := range map{}`

34. functions can be defined as`func funcName(input1 type1, input2 type2) (output1 type1, output2 type2) {}`, the return value names can be omitted

35. variadic functions can be defined as `func somename(arg ..int) {}`

36. functions are variables in go we can define them using `type` as `type typeName func(input1 inputType1 , input2 inputType2 [, ...]) (result1 resultType1 [, ...])` after that we can pass `typeName` function as a parameter type to some function, and the passing parameters function should be identical with the variable function with it's return type and input parameters.

37. `panic` breaks the normal flow of program and dives into panic status. when a function calls `panic` that function will stop executing at the point and the `defer` functions will start executing.

38. Golang has 2 retentions which are called `main, init` where `init` can be used in all packages and `main` can be used only in `main` package. These 2 functions are not able to have arguments or return values. We can write many `init` functions in one package(not recommended!) one `init` in a package.

39. every program initialize and begins it's execution from the `main`. if the `main` package imports other packages they will be imported at the compile time. If one packages is imported many times it will be compiled only once.  After importing packages programs will initialize the constants and variables within the imported packages, then execute the `init` function if it exists and so on. After all other packages are initialized, program will initialize constants and variables in the main package, then the `init` package will be executed if exist and then the `main`

40. go supports third-party packages in 2 ways, 1st relative path import `./moduel` 2nd absolute path import `$GOPATH/pkg/shorturl/model` 

41. `import ( . "fmt")` the dot operator can omits the package name when you call function inside that package. `fmt.Println("hello world")` becomes `Println(...)`

42. Alias operation changes the name of the package that we imported, `import ( f "fmt")` here `fmt.Println` will become `f.Println`

43. `import( _ "fmt")`, the `_` operator actually means we just want to import and execute the `init` function from the package.

44. user can define new types of containers with `struct`. `struct` is passed by value ways to define a `struct`

    ```Go
    P := person{"Tom", 25}
    P := person{age:24, name:"Bob"}
    P := struct{name string; age int}{"Amy",18}
    ```

45. `struct` in go can also has embedded fields, where fields from one `struct` can be imported to another `struct`

    ```go
    type Human struct {
        name string
        age int
        phone string
    }
    type engineer struct {
        Human // here all the fields of Human struct will be imported 
        YoE int
        phone string // user can access Human's phone by NA.Human.phone, to access the engineer's user can NA.phone
    }
    ```

46. Types defined by `struct` can have their methods, `func (someName RecieverType) funcName(params) (resutls)` is the way to define the method for some `ReceiverType` struct.

47. Receiver can be other then only `struct` type, `type typeName typeLiteral`. Customized types are similar to C

    ```go
    type age int
    type months map[string]int
    m := months { "jan": 31, .....}
    ```

48. If the name of methods are the same and their receivers are different then they are not same.

