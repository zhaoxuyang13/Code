### IntegriDB Build

---

**original instructions**https://github.com/integridb/Code

---

1. Dependencies, 比Github页面增加了libgmp-dev

   ```shell
   $ sudo apt-get install build-essential git libgmp3-dev libprocps3-dev libgtest-dev python-markdown libboost-all-dev libssl-dev libmysqlclient-dev mysql-server mysql-client libgmp-dev
   ```

2. Download and install xbyak

   ```shell
   $ git clone https://github.com/herumi/xbyak.git
   $ cd xbyak
   $ sudo make install
   ```

3. Download and make ate-pairing 

   ```shell
   $ git clone https://github.com/herumi/ate-pairing.git
   $ cd ate-pairing
   $ make
   ```

4. Download and install ntl library

   ```shell
   $ wget https://www.shoup.net/ntl/ntl-11.4.3.tar.gz
   $ gunzip ntl-11.4.3.tar.gz
   $ tar xf ntl-11.4.3.tar.gz
   $ cd ntl-11.4.3/src
   $ ./configure
   $ make
   $ make check
   /很久
   $ sudo make install
   ```

5. 环境变量

   ```shell
   $ export CPLUS_INCLUDE_PATH=$PWD/ate-pairing/include
   $ export LIBRARY_PATH=$PWD/ate-pairing/lib
   ```

6. 修改Makefile

   ```shell
   $ cp Makefile Makefile.copy
   
   $ sed -i 's/\/home\/ubuntu/pwd/g' Makefile  <= pwd改成当前的路径
   $ vim Makefile
   检查一下对不对，并修改LDFLAGS为
   	-lntl -lmysqlclient --std=c++0x -lssl -lcrypto -lpthread -lgmp
   $ gcc --version
   	gcc的版本不能太老，我编译成功的时候用的gcc8（原来镜像里面是gcc4.x)
   	https://askubuntu.com/questions/1028601/install-gcc-8-only-on-ubuntu-18-04
     
   ```

7. 设置table大小,修改文件 createtables.cpp.

   ``` shell
   $ make create
   $ ./createtables
   $ make main 
   $./main
   ```

   

   