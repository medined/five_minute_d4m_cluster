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
vagrant ssh master
accumulo_home/bin/accumulo/bin/start-all.sh
```
