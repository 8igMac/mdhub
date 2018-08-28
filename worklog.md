工作日誌
===

## 2018-08-13
:::info
### goal
1. run the test writtn by noreason
2. mimic the unit test file and parser api
:::

moring 9:00~12:41
- workstation ricing: i3-gaps
- visit JHHLAB website
- understand the work flow of google-unit-test
- trace Biovoltron/vcf/unit_test
- trace Neucleona lib: file structure
- make an ssh key and read some docs
- tried to build Biovoltron using cmake -> failed
afternoon 13:52~14:56(sleep)~16:40
- trace vcf unit test
- trace biovoltron file structor
night 18:00~19:00
- understand namespace

## 2018-08-14
:::info
### goal
1. ask about 
    - how to make
    - file structure
    - git
2. write unit test
2. impl the wiggle parser
:::

morning 10:26~13:00
- hunter debug -> still no clue(sth wrong with git), ask noreason
- practice git command and open a new wiggle branch in Biovoltron, ready to write unit_test
afternoon 13:45~17:52
- debug hunter with noreason(git submodule update, download hunter and nucleona) -> ask john?
- install cmake from source and try agagin
- update cmake solve the problem, I finally get to run vcf unit_test
:::info
final steps:
1. git clone Biovoltron
2. git submodule init
3. git submodule update
4. check cmake version >= 3.12.1
5. `$ mkdir Biovoltron/build`
6. `$ cd Biovoltron/build`
7. `$ cmake .. -DBUILD_TESTS=ON -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=../stage`
8. `$ make`
9. run the executable
:::
night 19:18~20:19
- add wig test data
- think about wig parser interface

## 2018-08-15 meeting day
:::info
### goal
1. vag display
2. unit test v0 -> send to teacher before noon
3. vbird linux tutorial
4. effective c++
:::

morning 8:55~12:20
- xrandr, vag setting done
- think about unit test interface

afternoon 13:20~17:10
- editing unit test v0
- making meeting slide 

night 19:30~20:40
- learn git merge request(pull request)

:::warning
## meeting note
- check doxygen
- pokemon/format/wig (legecy code)
- understand how to use wiggle file
- wrtie unit test
- documenting: write sth unit_test can't tell you(don't write interface)
:::

## 2018-08-16
:::info
### goal
1. get an example of .wig file
2. checkout doxygen doc
3. trach old version of wig parser - unit test
4. read effective c++
5. read v-bird linux tutorial 

night 18:00~
- checkout doxygen doc, understand some simple syntax
- checkout old pokemon wig parser.hpp (checked basic class member function)

## 2018-08-20
:::info
### goal
1. finish tracing john's wig parser
    - 
2. 1 chapter effective c++
3. 1 v-bird
:::

afternoon 13:40
