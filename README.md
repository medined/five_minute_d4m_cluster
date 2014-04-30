This project is a followup to the https://github.com/medined/Accumulo_1_5_0_By_Vagrant. That project used Vagrant to launch three virtual machines, then loads and configures the needed software. It takes about 30 minutes to provision the three virtual machines. Once the virtual machines were provisioned, I created .box files specific to VirtualBox to 'freeze' them.

This project shows how to use those .box files. Follow theses steps to get your own cluster working:

* Download the .box files. You'll need to pay S3 file transfer costs.

 <a href='https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-master.box'>https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-master.box</a>

 <a <href='https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-slave1.box'>https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-slave1.box</a>

 <a href='https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-d4m.box'>https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-d4m.box</a>

* Add the three boxes to Vagrant.

```
vagrant box add -f affy-master affy-master.box
vagrant box add -f affy-slave1 affy-slave1.box
vagrant box add -f affy-slave2 affy-slave2.box
```

* Spin-up the instances.

```
vagrant up
```

* Run the post-spin script.

```
./post_spinnup.sh
```

* Follow the instructions from the script to start Accumulo.

```
vagrant ssh slave2
accumulo_home/bin/accumulo/bin/start-all.sh
```

* Now you are free to use D4M:

```
vagrant@affy-slave2:~$ octave
GNU Octave, version 3.8.1
Copyright (C) 2014 John W. Eaton and others.
This is free software; see the source code for copying conditions.
There is ABSOLUTELY NO WARRANTY; not even for MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE.  For details, type 'warranty'.

Octave was configured for "x86_64-unknown-linux-gnu".

Additional information about Octave is available at http://www.octave.org.

Please contribute if you find this software useful.
For more information, visit http://www.octave.org/get-involved.html

Read http://www.octave.org/bugs.html to learn how to submit bug reports.
For information about changes from previous versions, type 'news'.

octave:1> addpath('/home/vagrant/accumulo_home/bin/d4m_api/matlab_src')
octave:2> Assoc('','','');
octave:3> DBinit;
octave:4> hostname='affy-master';
octave:5> cb_type = 'Accumulo';
octave:6> instance_name='instance';
octave:7> username = 'root';
octave:8> password = 'secret';
octave:9> DB = DBserver(hostname,cb_type,instance_name, username, password)
Database Object

  scalar structure containing the fields:

    host = affy-master
    type = Accumulo
    instanceName = instance
    user = root
Tables in database:
Variables in the current scope:

   Attr Name          Size                     Bytes  Class
   ==== ====          ====                     =====  =====
        METADATA      1x1                         70  DBtable
        trace         1x1                         66  DBtable

Total is 2 elements using 136 bytes
octave:10> ls(DB)
ans = !METADATA trace
```

## Making life easier

First export some variables that hold information about your Accumulo instance. You might want to place these into your .bashrc file with adequate permissions.

```
export ACCUMULO_PASSWORD=secret
export ACCUMULO_USER=root
export ACCUMULO_INSTANCE=instance
export ACCUMULO_HOST=affy-master
```

Now create a .octaverc file with the following:

```
addpath('/home/vagrant/accumulo_home/bin/d4m_api/matlab_src')
Assoc('','','')
DBinit
hostname = getenv('ACCUMULO_HOST')
instance_name = getenv('ACCUMULO_INSTANCE')
username = getenv('ACCUMULO_USER')
password = getenv('ACCUMULO_PASSWORD')
DB = DBserver(hostname,'Accumulo', instance_name, username, password)
disp("\nCustom initialization complete. Use 'DB' to access Accumulo!\n")
```

Now each time that Octave is started, the Accumulo connection will be immediately ready for use.

