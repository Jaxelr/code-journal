# Sql Server model database

The model database basically serves as a "model" for the subsequent created databases. It includes the creation of tempdb (which happens on any Sql Server Restart) and the rest of the persisten databases. 

For example, configuring the model DB Recovery model to Simple will result on the subsequent databases created being configured by default with the DB Recovery model of Simple.

This applies to files, file groups and options.
