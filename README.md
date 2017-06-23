# AC3.2-APIs-II

>>>> TODO
1. Remove part 2 files to this repo
2. after saving the sample solutions, delete branches from part 1


---
### Solutions Table of Contents:

> Todo: Only part 1

1. Part 1
  1. [Exercise Problem #1](https://github.com/C4Q/AC3.2-APIs/commit/eac9a12b045b9d8e429bea2455d8f464dc6df856)
  2. [Exercise Problem #2](https://github.com/C4Q/AC3.2-APIs/commit/95d7ff70877ecfae063ca54535e3f4e44366be02)
  3. [Exercise Problem #3](https://github.com/C4Q/AC3.2-APIs/commit/360b01f2c471790af8e9785abb0afa755e0ccbb3)
  4. [Advanced Solution](https://github.com/C4Q/AC3.2-APIs/commit/50ea9acef5f4b02a99a9adc12f079b36570d08b5)
  5. [Expert Solution](https://github.com/C4Q/AC3.2-APIs/commit/031933e726c840aeab8682ce46edcff09382997b)


2. Part 2
  1. [Start of Project](https://github.com/C4Q/AC3.2-APIs/tree/2_part_II_setup)
  2. [Full Solutions (Part 1 & 2)](https://github.com/C4Q/AC3.2-APIs/tree/2_full-solutions)
  3. Answers to [ExercisesREADME](https://github.com/C4Q/AC3.2-APIs/blob/master/Part%20II/ExercisesREADME.md) exercises (TBD)
3. Part 3
  1. [Final code for lesson](https://github.com/C4Q/AC3.2-APIs/tree/3_userDefaults)
  2. Answers for exerices (TBD)

Note: The exercises outlined in [ExercisesREADME](https://github.com/C4Q/AC3.2-APIs/blob/master/Part%20II/ExercisesREADME.md) are not all covered, even in the "Full Solution" link. 

>>> This should be the next lesson:

1. how to build request
2. Exercise on building request functions
3. Exercise on re-writing to use default parameters
4. Advanced on next section is for the URL factory method

#### Handling Errors
As you parse out the `Any` object into arrays and dictionaries, I would recommend adding `print` statements along the way to see where something is working or failing

---
### Exercises

#### 1. More Requests
Create three more functions for our `APIManager`:

1. `func getRandom(users: Int, completion: ((Data?)->Void) )`
2. `func getRandom(users: Int, gender: UserGender, completion: ((Data?)->Void) )`
3. `func getRandom(users: Int, nationality: UserNationality, completion: ((Data?)->Void) )`

For each of these, the `users` parameter will be an `Int` that will change the number of results returned on an API call. `UserGender` and `UserNationality` should be two `enum` that correspond to the possible options as listed in the RandomUserAPI documentation (including a "no-preference" option). 

<details><summary>Code Hints</summary>

<ol>
<li> Your enums will look like this: <code>enum UserGender: String { ... }</code> and <code>enum UserNationality: String { ... }</code>
<li> Constructing URL's is more easily done by starting off with a <code>String</code> and then later using <code>URL(string:)</code> when the string is ready.
<li>Pay attention to the documentation on making requests with parameter. 
</ol>

</details>

__Advanced__

Using default parameter values, find a way to condense **all** of the four functions we now have in `APIManager` into just one.

#### Resources for Advanced: 

1. [Why You should love default parameter values - Natasha the Robot](https://www.natashatherobot.com/swift-default-parameter-values/)
2. [Parameter Defaults and Optional Function Parameters](https://craiggrummitt.com/2016/06/29/parameter-defaults-and-optional-function-parameters-in-swift-3-0/)

__Expert__

Create a separate "factory" class to generate the appropriate `URL` given the different possible parameters of `users`, `nationality` and `gender`. Call this factory `RandomUserURLFactory` with a singleton called `manager`. This factory class is intended to be used by the `APIManager`.

`RandomUserURLFactory` will have one function: `func endpoint(users: Int, nationality: [UserNationality], gender: UserGender) -> URL`. From those parameters, build an appropriate URL to make a request. There are no particular rules on how you should go about doing this, so feel free to explore code. Just be sure to use Postman to test URLs and make sure you have an understanding of the format of the parameters.

Examples:

| | |
|---|---|
|Input|`RandomUserURLFactory.manager.endpoint(users: 10, nationality: [.GB], gender: .male)`|
|Output| `https://randomuser.me/api/?results=10&nat=GB&gender=male` |

| | |
|---|---|
|Input| `RandomUserURLFactory.manager.endpoint(users: 2, nationality: [.AU,.BR,.GB], gender: .noPreference)` |
|Output| `https://randomuser.me/api/?results=2&nat=AU,BR,GB&gender=` |
