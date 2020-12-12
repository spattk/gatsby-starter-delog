---
template: BlogPost
path: /openjdk14-ubuntu16.04
date: 2020-12-12T11:03:35.838Z
title: Installing OpenJDK 14 on Ubuntu 16.04
---
There are many tutorials to install OpenJDK 14 on Ubuntu 18.04 and 20.04.\
But I found it difficult to find a working one for Ubuntu 16.04. Please follow the steps to make it work on your machine.

**1. Going to the correct location and create directory**

Though it can be installed anywhere but it is recommended to have it at the following location.

```
sudo mkdir /usr/java
cd /usr/java
```

**2. Downloading the JDK**

```
curl https://download.java.net/java/GA/jdk14.0.2/205943a0976c4ed48cb16f1043c5c647/12/GPL/openjdk-14.0.2_linux-x64_bin.tar.gz --output openjdk-14.tar.gz
```

This command will download the openjdk-14.0.2 from java.net.\
If you want to have more updated version, just refer the website to get the correct version and rename it here.

**3. Extracting the compressed file**

```
sudo tar -xzvf openjdk-14.tar.gz
```

It would have created a directory jdk-14.0.2/

**4. Setting the path**

I highly recommend to use zsh for terminal.\
If you are on zsh, please do the following steps the following steps to ~/.zshrc file.

```
mv jdk-14.0.2 jdk-14
vi ~/.zshrc
```

Append the lines in the last of the opened file

```
export JAVA_HOME=/usr/java/jdk-14
export PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
```

```
source ~/.zshrc
```

**5. Checking the version**



```
java -version
```

You should get something like the following

```
openjdk version "14.0.2" 2020-07-14
OpenJDK Runtime Environment (build 14.0.2+12-46)
OpenJDK 64-Bit Server VM (build 14.0.2+12-46, mixed mode, sharing)
```

**6. We are done. Happy coding in Java**
