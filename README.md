# mysql_static_msvc
Static Library for Microsoft Visual Studio

1) Goto https://downloads.mysql.com/archives/community/ and Download Desire Version. Sample is Version 5.7.28

![image](https://user-images.githubusercontent.com/17219341/132113423-1518106c-c8c5-4cf5-a0ff-082c4f4979b4.png)

2) For build from source, you must need openssl static build so you can download from https://www.openssl.org/source/. You can use any desire version. In sample choose 1.1.1l

![image](https://user-images.githubusercontent.com/17219341/132113469-5039c11d-0cdf-44b3-a039-3ef8de905d05.png)

3) Need to build openssl, so follow https://github.com/RayMarmAung/openssl-1.1.1k_vs_static
4) Extract mysql-5.7.28 to desired directory. For example C:\sql\mysql-5.7.28

![image](https://user-images.githubusercontent.com/17219341/132113524-e4f33428-deb3-4a6a-acf1-8802981cfc92.png)

5) Need CMake, download from https://cmake.org/download/ , install and set environment path to this
6) Launch Developer Command Prompt for VS 2017 as admin, you can use any VS version
7) Change to mysql src directory 

![image](https://user-images.githubusercontent.com/17219341/132113570-300f314e-2635-45f6-a63a-48400af9ec2a.png)

8) Type CMake command like this 

cmake -Bc:\mysql -DBUILD_SHARED_LIBS=OFF -DLINK_STATIC_RUNTIME_LIBRARIES=1 -DDOWNLOAD_BOOST=1 -DWITH_BOOST="C:\Boost" -DCMAKE_CXX_FLAGS_RELEASE="/MT" -DWITH_SSL="C:\openssl32_msvc" -G "Visual Studio 15 2017"

-B is build path, -DWITH_SSL is your previous built openssl path, make sure build with /mt flag, -G is compilar, if need 64 bit, type "Visual Studio 15 2017 Win64"
And wait a while to finish

![image](https://user-images.githubusercontent.com/17219341/132113660-8359ba73-59dd-4b25-b341-b6a0680ff28d.png)

9) After finished, goto cmake build path and find MySQL.sln (for example- c:\mysql\MySQL.sln). and open it with visual studio 
10) Then Build ALL_BUILD with RelWithDebInfo

![image](https://user-images.githubusercontent.com/17219341/132113730-5360324d-709d-4114-8f57-e577de575507.png)

11) After finish, you will find mysqlclient.lib in cmake build in archive_output_directory\RelWithDebInfo directory

![image](https://user-images.githubusercontent.com/17219341/132113786-e2f0e1b6-7280-4df8-a6d0-ceceb403a840.png)

P.S - this library links with these standard libs 
- advapi32
- user32
- crypt32
- gdi32

These libraries are necessary to declare when you build Qt Static Build
