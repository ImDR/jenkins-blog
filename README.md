# Jenkins: what is it?

Jenkins is a continuous integration software tool. It is an open source software, developed using the Java programming language. It allows you to test and report changes made over a large code base in real time. By using this software, developers can detect and solve problems in a codebase and quickly. Thus the tests of new builds can be automated, which makes it easier to integrate changes to a project, on an ongoing basis. Jenkin's goal is to accelerate software development through automation. Jenkins enables the integration of all stages of the development cycle.

Continuous integration is provided through plugins. These plugins allow the integration of various stages of Various DevOps. To integrate a particular tool, it is necessary to install the plugins corresponding to this tool: Git, Maven 2 project, Amazon EC2, HTML Publisher


## What are the benefits of Jenkins?

Jenkins has several advantages. It is an open source tool that federates a large community, constantly proposing new improvements and other improvements. The software is easy to install, and over 1000 plugins are available. If a plugin that fits your needs does not exist, you can create it yourself and share it with the community. Another advantage: Jenkins is also free. Finally, as a tool developed with Java, it can be ported to all major software platforms.

In addition, Jenkins differs from most other multi-point continuous integration tools. First of all, Jenkins is adopted much more widely than its competitors. In total, there are 147,000 active installations and more than one million users around the world. Jenkins' other strength is its interconnection with over 1000 plugins to integrate with most development, testing and deployment tools.

## Installation of Jenkins

Install Jenkins (one of the software used as a foundation for a continuous integration platform - and the most used currently for PHP projects), if you have an integration server to date, is not very complicated : the basic idea is to download a .war, and launch it; possibly adding this launch to machine services, so that it is automated.


#### Under Ubuntu

Use the Ubuntu distribution on your development machines and on your integration servers. The installation of Jenkins under Ubuntu is extremely simple.

You have just four lines of commands to run to install Jenkins:

`wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -`

`sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'`

`sudo apt-get update`

`sudo apt-get install jenkins`

#### And under Windows?

This is usually not very useful in a PHP project (although, depending on the type of project, check its operation under a wide range of OS is not a bad idea at all), but Jenkins can also to be installed on Windows.

Download and install Jenkins from https://jenkins.io

![Website](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/screenshot-website.jpg "")

### Once Jenkins is installed?

Once Jenkins is installed, all you have to do is access your interface via your web browser.

By default, Jenkins listens on port 8080; therefore, depending on the address of your integration server, you will use a URL of this type to access it:

`http://localhost:8080`

Or,

if you have defined a DNS entry or alias in your hosts file, you will use something like this:

`http://jenkins:8080`

### Quick tour of the administration interface, and basic management

Now that we have Jenkins installed, and we know how to access them, let's take a quick tour of the admin interface, before we start installing the plugins that will later be used for the Continuous Integration of a PHP project.

First, if we point our browser to port 8080 of our integration server (in my case, http://localhost:8080), we come to the Jenkins homepage:

![screenshot 1](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_001-just-installed-admin-screen_m.png "")

Here we can note some first elements:

+ In the top left, the main menu, from which we can administer Jenkins, add users, ...
+ Just below, still to the left, the construction queue, which will eventually indicate projects pending / under construction,
+ And, of course, in the middle of the screen, since we have not created a job yet, a link inviting us to do it.

Clicking the `Administer Jenkins` link on the left menu will take you to the management page of our Continuous Integration platform:

![screenshot 2](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_002-just-installed-manage-screen_m.png "")

I encourage you to click on the first entry on this page, the `Configure System` link, which will allow you to configure the general settings of the platform:

![screenshot 3](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_003-just-installed-manage-configure-system-01_m.png "")

As you can see, the list of available options is already relatively long, since it does not usually fit on one screen:

![screenshot 4](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_003-just-installed-manage-configure-system-02_m.png "")

Fortunately, you will find, for almost every Jenkins option and setting, a "Help" button on the right side of the screen.
Clicking it will display some information about the data expected by the form field next to which this icon appears.


For example, if I click on the "Help" button to the right of the "Waiting Period" field:

![screenshot 5](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_003-just-installed-manage-configure-system-03-help-01_m.png "")

As is, there is not much to configure: the default options tend to do the trick.


That said, I can only advise you to take the time to read the help of each option: this will allow you to see what you can do with Jenkins, as well as familiarize yourself with the platform.

In the same spirit, do not hesitate to take a look at the other screens of the administration interface: after all, a little curiosity has never hurt ;-)

### Installing plugins

A great wealth of Jenkins (which, basically, does not do much - especially in terms of PHP projects) is its system of plugins, as well as the large number of existing plugins.

To access the plugin management screens: Manage Jenkins> Manage Plugins, which should take you to `http://localhost:8080/pluginManager/`.

Here, you will have before you the list of installed plugins (some plugins are provided with Jenkins, and, therefore, already installed, even if it is not by you), for which an update is available:

![screenshot 6](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_004-just-installed-manage-plugins-01-updates-available_m.png "")

The next-to-side tab is the one that lists the available plugins, more or less categorized - as you can see, the list is long; and going through it quickly can give you an idea of ​​the real possibilities of a Jenkins Continuous Integration Platform:

![screenshot 7](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_004-just-installed-manage-plugins-02-available_m.png "")

Let's continue with the third tab, which displays the list of installed tabs.
For the moment, there are only a few, but we will quickly extend this list:

![screenshot 8](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_004-just-installed-manage-plugins-03-installed_m.png "")

And finally, a fourth tab "Advanced", which will allow you, if necessary, to configure a Proxy, by which Jenkins will pass for downloading plugins or looking for updates:

![screenshot 9](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_004-just-installed-manage-plugins-04-advanced_m.png "")

### Configuration?

Now that our Jenkins Continuous Integration Platform is installed, with all the plugins we will need for our PHP projects, all we have to do is configure it, before we can switch to IC implementation. a PHP project.

#### System configuration
We'll go back to the "Administer Jenkins> Configure the System" screen that we've been looking at above, and review some of the configuration items that may be interesting - knowing that much depends on it of your needs.


First, Jenkins allows you to configure who can access the platform, how, and what types of manipulations are allowed:

![screenshot 10](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_007-configure-01-security-access_m.png "")


Depending on your policy, you will choose to give all potential users access to all features, or you configure Jenkins so that only administrator accounts can access certain operations.

Do not forget two things, all the same:

- The success of Continuous Integration relies in part on the involvement of all members of the team,
- If your server is open on the Internet, you may not want to make it public ;-)

If you have installed the plugin SCM Sync plugin plugin, seen above, you will have the possibility to save the configuration of your IC platform to a versioning server; this can potentially be interesting, if only to facilitate the cancellation of insufficiently thought-out modifications:

![screenshot 11](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_007-configure-02-scm-sync-configuration_m.png "")

Then, for those of you who are going to work with projects under SVN, it can be interesting to configure the version of SVN emulated by Jenkins (in particular, if you want to be able to work with other tools on the extraction made by Jenkins):

![screenshot 12](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_007-configure-03-svn_m.png "")

Depending on the projects, the teams, and the attention that everyone pays to the emails, you may want to set up a little more reporting by email:

![screenshot 13](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_007-configure-04-extended-email-notification_m.png "")

Note that e-mail notifications can also be enabled / configured per project.


Finally, in the event that your Jenkins platform will have to connect to other machines via SSH, you will probably want to configure an SSH key for Jenkins:

![screenshot 14](https://raw.githubusercontent.com/ImDR/jenkins-blog/master/screenshots/_007-configure-05-ssh-key_m.png "")

Example of use: push in SSH / SCP the result of the build to a reporting server; or deploy at each successful integration an archive containing the source code corresponding to it.
