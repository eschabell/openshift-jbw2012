JBoss Keynote Demo from JBossWorld 2012 Quickstart Guide
========================================================

Demo based on JBoss EAP6 and the existing code base of the Keynote demo.

Setup and Configuration
-----------------------
Create an account at http://openshift.redhat.com/

Create a jbosseap-6.0 application that scales and is of medium gear size.

$ rhc app create -a jbw2012 -t jbosseap-6.0 -g medium -s

Add this upstream openshift-jbwkeynote-2012 repo

$ cd editor
$ git remote add upstream -m master git://github.com/eschabell/openshift-jdwkeynote-2012.git
$ git pull -s recursive -X theirs upstream master

Then push the repo upstream.

$ git push

We also need to push some of the configuration files for drools-guvnor. To do this you need to know the UUID of your machine, you
can find this with:

$ rhc domain show

jbw2012
    Framework: jbosseap-6.0
     Creation: 2012-09-17T12:51:12-04:00
         UUID: [some-number]
      Git URL: ssh://[some-number]@jbw2012-$yourdomain.rhcloud.com/~/git/jbw2012.git/
   Public URL: http://jbw2012-$yourdomain.rhcloud.com/
   Cartridges:
       haproxy-1.4

Use the UUID to scp the following files:

$ scp support/guvnor-roles.properties [UUID]@jbw2012-$yourdomain.rhcloud.com:jbosseap-6.0/jbosseap-6.0/standalone/configuration/
$ scp support/guvnor-users.properties [UUID]@jbw2012-$yourdomain.rhcloud.com:jbosseap-6.0/jbosseap-6.0/standalone/configuration/
$ scp support/standalone.xml [UUID]@jbw2012-$yourdomain.rhcloud.com:jbosseap-6.0/jbosseap-6.0/standalone/configuration/

That's it, you can now checkout your application at:

http://jbw2012-$yourdomain.rhcloud.com

Accessing the Client Applications

buyer application: jbw2012-$yourdomain.rhcloud.com/jbossworld-client

approver application: jbw2012-$yourdomain.rhcloud.com/jbossworld-client/#approver  (password is letmein)

VP application: jbw2012-$yourdomain.rhcloud.com/jbossworld-client/#vp    (password is letmein)

Note: To switch between roles, you must first logout. Once logged out, you will not be able to return to the previous role so a new
role will be created when you log in again.  

jbw2012-$yourdomain.rhcloud.com/jbossworld-client/#logout

You can also look at the drools-guvnor via: jbw2012-$yourdomain.rhcloud.com/drools-guvnor (login admin/admin).

PROBLEMS: seems like standalone.xml is being overwritten so admin/admin login not working.

Enjoy!

