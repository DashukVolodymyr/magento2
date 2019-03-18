---
group: installation-guide
subgroup: Prerequisites
title: Prerequisites
menu_node: parent
menu_title: Prerequisites
menu_order: 1
functional_areas:
  - Install
  - System
  - Setup
---

## Before you begin {#instgde-prereq-overview}

Before you install Magento, you must do all of the following:

*	Set up one or more hosts that meet the [Magento system requirements]({{page.baseurl}}/install-gde/system-requirements.html).
*	If you are setting up more than one web node with load balancing, set up and test that part of your system _before_ you install Magento.
*	Make sure you can back up your entire system at various points during the installation so you can roll back in the {% glossarytooltip c57aef7c-97b4-4b2b-a999-8001accef1fe %}event{% endglossarytooltip %} of issues.

{:.bs-callout .bs-callout-info}
We assume you're installing the Magento 2 software in a <em>development environment</em>, which means you have [root user](http://www.linfo.org/root.html) access to the machine <em>and</em> that the machine does not need to be highly secure. If you're setting up a more secure machine, we strongly recommend you consult a network administrator for additional assistance.

We strongly recommend you update and upgrade your operating system software. These upgrades can provide security and software fixes that might prevent future problems. Don't know what any of this means? Check out our [installation overview page]({{page.baseurl}}/install-gde/bk-install-guide.html).


Enter the following commands as a user with `root` privileges:

*	Ubuntu

		apt-get update
		apt-get upgrade

*	CentOS

		yum -y update
		yum -y upgrade

## Prerequisite check {#instgde-prereq-check}

To check your system for prerequisites, enter the following commands:

### Apache

CentOS: `httpd -v`

Ubuntu: `apache2 -v`

You must run Apache version 2.2 or 2.4 as the following result indicates:

	Server version: Apache/2.2.15 (Unix)
	Server built:   Jul 23 2014 14:17:29

To install or upgrade Apache, see [Apache]({{page.baseurl}}/install-gde/prereq/apache.html).

### PHP

{:.bs-callout .bs-callout-info}
Magento, with assistance from our community, implemented PHP 7.2 compatibility for our [2.3.0 release](/guides/v2.3/release-notes/bk-release-notes.html). Any backward-incompatibility issues are resolved in this release, and all 3rd party libraries now support PHP 7.2. Fully tested 7.2 support will be delivered in following patch releases. If you are interested in participating in Magento Community projects we welcome your help! See our [ZenHub board](https://app.zenhub.com/workspace/o/magento-engcom/php-7.2-support/boards?repos=116423356,116426364,115111902) for a full list of outstanding issues.

	php -v

You must run {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %} version 7.1.x or 7.2.x as the following result indicates:

	PHP 7.1.6 (cli) (built: Jan  9 2017 09:23:16) ( NTS )
    Copyright (c) 1997-2017 The PHP Group
    Zend Engine v3.1.0, Copyright (c) 1998-2017 Zend Technologies with Zend OPcache v7.1.6, Copyright (c) 1999-2017, by Zend Technologies

See [PHP](/guides/v2.3/install-gde/prereq/php-centos-ubuntu.html) for info on installing PHP for CentOS or Ubuntu.

### MySQL

	mysql -u <database root user or database owner name> -p

For example:

	mysql -u magento -p

You must run MySQL version 5.6 or later as the following result indicates:

		Welcome to the MySQL monitor.  Commands end with ; or \g.
		Your MySQL connection id is 871
		Server version: 5.6.21 MySQL Community Server (GPL)

		Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

		Oracle is a registered trademark of Oracle Corporation and/or its
		affiliates. Other names may be trademarks of their respective
		owners.

		Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

Enter `exit` at the `mysql>` prompt to exit.

To install or upgrade MySQL, see [MySQL]({{page.baseurl}}/install-gde/prereq/mysql.html).

#### Next step

[Choose how to install the Magento software]({{page.baseurl}}/install-gde/bk-install-guide.html)

#### Related topics

*	[MySQL]({{page.baseurl}}/install-gde/prereq/mysql.html)
*	[Apache]({{page.baseurl}}/install-gde/prereq/apache.html)
*	[PHP&mdash;Ubuntu]({{page.baseurl}}/install-gde/prereq/php-centos-ubuntu.html#php-for-ubuntu)
*	[PHP&mdash;CentOS]({{page.baseurl}}/install-gde/prereq/php-centos-ubuntu.html#php-for-centos)
*	[Installing optional software]({{page.baseurl}}/install-gde/prereq/optional.html)
*	[How to get the Magento software]({{ page.baseurl }}/install-gde/bk-install-guide.html)