intellij-decrypt
================

Small utility to decrypt passwords saved by Intellij IDEA / Android Studio. It works for passwords you forgot but they are still stored (encrypted) by Intellij IDEA / Android Studio. You have to supply the master password and the path to the security.xml file.

Usage
-----
Find your Intellij IDEA / Android Studio security.xml files (for Linux, OSX):

    cd
    find . | grep "security\.xml"

Run the following from a terminal and follow the instructions (for Linux, OSX):

    git clone git@github.com:sebasbad/intellij-decrypt.git
    cd intellij-decrypt
    mkdir -p ./src/com/intellij/ide/passwordSafe/impl/providers/
    curl https://android.googlesource.com/platform/tools/idea/+/snapshot-master/platform/platform-impl/src/com/intellij/ide/passwordSafe/impl/providers/EncryptionUtil.java?format=TEXT | base64 -D > ./src/com/intellij/ide/passwordSafe/impl/providers/EncryptionUtil.java
    curl http://archive.apache.org/dist/commons/codec/binaries/commons-codec-1.9-bin.tar.gz -o ./lib/commons-codec-1.9-bin.tar.gz
    tar -xzf ./lib/commons-codec-1.9-bin.tar.gz -C ./lib/
    javac ./src/org/corneliudascalu/intellijdecrypt/Main.java -classpath .:lib/commons-codec-1.9/commons-codec-1.9.jar:./src
    java -classpath .:lib/commons-codec-1.9/commons-codec-1.9.jar:src org.corneliudascalu.intellijdecrypt.Main -p your_master_password -f /your/path/to/security.xml

License
-----
Copyright 2014 Corneliu Dascalu

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
