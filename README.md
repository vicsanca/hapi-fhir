hapi-fhir
=========

HAPI FHIR - Java API for HL7 FHIR Clients and Servers

Complete project documentation is available here:
http://jamesagnew.github.io/hapi-fhir/

A demonstration of this project is available here:
http://fhirtest.uhn.ca/



Creating your own demo server with Vagrant
========
This source code repository includes configuration files to materialize an _entire_ server implementation in a single virtual machine (VM) image from scratch, allowing you to quickly bootstrap your own instance. The server will be completely encapsulated within the created VM image. The process _should_ run on OSX, Linux and Windows, but YMMV. The built-in settings support creation of a *VirtualBox*-based image on Ubuntu Linux, though with tuning the base image you should be able to create images suitable for other hypervisors and cloud-based IaaS providers such as VMware and Amazon Web Services (AWS), respectively.

Dependencies
----

Prior to running, please ensure you have all .war files built, and the following installed and functioning propertly.

 * All normal Java development dependencies. (SDK and Maven, specifically.)
 * VirtualBox
 * Vagrant


Creating Your VM
----

    cd hapi-fhir-root/
    mvn install # Creates web application .war files. Make sure they're built before proceeding!
    vagrant up # Will take a few minutes to boot up.

Your new server environment should now be running in a headless virtual machine on your local computer. The following step are performed automatically for you within the VM sandbox environment:

 * A complete Ubuntu 14.04 Server VM is launched in headless mode, bridged to whatever host network interface you've selected.
 * An IPv4 address is assigned via DHCP.
 * MySQL Server (Community Edition) is installed from the official 10gen repository. (See the [Vagrantfile](https://github.com/preston/hapi-fhir/blob/master/Vagrantfile) for the default root password.)
 * Oracle Java 8 is installed.
 * Tomcat 7 is installed and configured as a system service.
 * All compiled *.war applications are deployed automatically and started.
 * A "fhir" user is added to tomcat-users.xml. See [fhir.json](https://github.com/preston/hapi-fhir/blob/master/chef/data_bags/tomcat_users/fhir.json) for the default password.

The Vagrant documentation is the best place to start, but a few more commands of note are:

    vagrant ssh # Command-line access to the VM.
    vagrant destoy # Shuts down and completely destroys the VM.


Credits
----
Vagrant and Chef configuration by Preston Lee <preston.lee@prestonlee.com>
