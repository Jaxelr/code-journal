# Installing web deploy on a new IIS

From server manager:

![server](images/servermanager1.jpg)

Install the latest web platform installer:

![iis](images/iis1.jpg)

![iis-2](images/iis2.jpg)

Restart the server after.

Go to service manager in IIS and proceed to configure the allow remote connections, server certificate (if needed):

![iis-3](images/iis3.jpg)

![iis-4](images/iis4.jpg)

This completes the server side configuration, now you can configure the client side publish profile as usual, using the option of Web deploy.

