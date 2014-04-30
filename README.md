
This project is a followup to the https://github.com/medined/Accumulo_1_5_0_By_Vagrant. That project used Vagrant to launch three virtual machines, then loads and configures the needed software. It takes about 30 minutes to provision the three virtual machines. Once the virtual machines were provisioned, I created .box files specific to VirtualBox to 'freeze' them.

This project shows how to use those .box files. Follow theses steps to get your own cluster working:

1. Download the .box files. You'll need to pay S3 file transfer costs.
 ** <a href='https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-master.box'>https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-master.box</a>

 ** <a <href='https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-slave1.box'>https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-slave1.box</a>

 ** <a href='https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-d4m.box'>https://s3.amazonaws.com/accumulo.1.5.0.by.vagrant/affy-d4m.box</a>

