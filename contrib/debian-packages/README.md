ossec-debian
=====

Description
-----
OSSEC is an Open Source Host-based Intrusion Detection System that performs log analysis, file integrity checking, policy monitoring, rootkit detection, real-time alerting and active response.

These are the files used to create OSSEC-HIDS version 2.8.2 debian packages, the ones included both in ossec.net website and in WAZUH repository. You can find these packages at:

http://www.ossec.net/?page_id=19

or directly at: http://ossec.wazuh.com/repos/apt/

There are two different packages that can be built with these files:

* ossec-hids: Package that includes both the server and the agent.
* ossec-hids-agent: Package that includes just the agent.

Contents
-----
Contents of contrip/debian-packages
Each one of the subdirectories includes:

* Patches
* Debian control files: changelog, compat, control, copyright, lintian-overrides, postinst, postrm, preinst, rules

Additionally a script, ```generate_ossec.sh```, is included to generate the Debian packages for Jessie, Sid and Wheezy Debian distributions, both for i386 and amd64 architectures. This script uses Pbuilder to build the packages, and uploads those to an APT repository, setup with Reprepro.

Pre-Reqs and Usage Guide:
-----
This is a work in progress and is not a committment:
* Debian Control files must be placed in the control file location defined in the ```generate_ossec.sh``` script.
    * /home/ubuntu/debian_files/${ossec_version}/$package/debian
    * Please create these directories, and copy the debian control files: Example if working from the same directory as this file in git.

<pre><code>mkdir -p /home/ubuntu/debian_files/2.8.2/ossec-hids/
mkdir -p /home/ubuntu/debian_files/2.8.2/ossec-hids-agent/
cp -pr contrib/debian-packages/ossec-hids/debian/ /home/ubuntu/debian_files/2.8.2/ossec-hids/
cp -pr contrib/debian-packages/ossec-hids-agent/debian/ /home/ubuntu/debian_files/2.8.2/ossec-hids-agent/
</code></pre>

* Pbuilder must be installed
``apt-get install pbuilder```
    * And must have base images built
    ```pbuilder create```


Issues and Ideas
-----
This is a work in progress and is not a committment:
* Upgrade to 2.9.0
* Design ```generate_ossec.sh``` to use either pre-deployed control files, or use those which come packaged with the source.
* Develop step-by-step instructions for anyone to take a base install of debian/ubuntu and generate packages.
    * Add ossec-hids-server, ossec-hids-hybrid, and ossec-hids-agent. Primary work will be on successful ossec-hids-agent.
    * Add option to set server IP during build. Useful for agent, and hybrid.
    * Add option to include CA Certificates for agent-auth/authd
    * Consider possibilities around other PKI requirements.

Further Reading
-----

For more details on how to create Debian Packages and an APT repository you can check my post at:

http://santi-bassett.blogspot.com/2014/07/setting-up-apt-repository-with-reprepro.html

Please don't hesitate to contribute (preferably via pull requests) to improve these packages.
