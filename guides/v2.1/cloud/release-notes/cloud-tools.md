---
group: cloud-guide
title: Release notes for ece-tools
functional_areas:
  - Cloud
  - Setup
  - Configuration
redirect_from:
   - /guides/v2.1/cloud/release-notes/CloudReleaseNotes.html
---


<!-- Assigning liquid variables for placeholder values
{% assign base_url = "{{base_url}}" %}
{% assign unsecure_base_url = "{{unsecure_base_url}}" %}
-->

The `{{site.data.var.ct}}` package is compatible with {{site.data.var.ee}} version 2.1.4 and later to provide a rich set of features you can use to manage your {{site.data.var.ece}} project. It contains scripts and {{site.data.var.ece}} commands designed to help manage your code and automatically build and deploy your projects.

You can list the available `{{site.data.var.ct}}` commands using:

```bash
php ./vendor/bin/ece-tools list
```

The following updates describe the latest improvements to the `{{site.data.var.ct}}` package, which uses the following version sequence: `200<major>.<minor>.<patch>`. See [Upgrades and patches]({{ site.baseurl }}/guides/v2.1/cloud/project/project-upgrade-parent.html) for information about updating to the latest release of the `{{site.data.var.ct}}` package.

The release notes include:

-   {:.new}New features
-   {:.fix}Fixes and improvements

## v2002.0.15

-   {:.new}**Docker Updates**—

    -   <!-- MAGECLOUD-2888 -->Now the Docker generator uses the services specified in the `.magento.app.yaml` and `.magento/services.yaml` configuration files when [building your Docker environment]({{page.baseurl}}/cloud/docker/docker-config.html). You can choose a different service version using build parameters.

    -   <!-- MAGECLOUD-2799 -->Added PHP 7.2 image—Added support for PHP 7.2 in Cloud Docker; updated the [Launch Docker configuration]({{ page.baseurl }}/cloud/docker/docker-config.html) to include the `docker:build --php` option to specify the version of PHP compatible with your Magento Commerce version.

    -   <!-- MAGECLOUD-2565 -->Added a [Cron container]({{page.baseurl}}/cloud/docker/docker-development.html#cron-container) based on the PHP-CLI image.

    -   Added the following services to the Docker build:

        -   <!-- MAGECLOUD-2567 & 2889-->RabbitMQ 3.5 and 3.7

        -   <!-- MAGECLOUD-2569 & 2887 -->ElasticSearch 1.7, 2.4, and 5.2

        -   <!-- MAGECLOUD-2886 -->Redis 3.2 and 4.0

    -   <!-- MAGECLOUD-2577 -->Now you have the DB dump capability when using the Cloud Docker [database container]({{page.baseurl}}/cloud/docker/docker-development.html#database-container). Also, you can [share files]({{page.baseurl}}/cloud/docker/docker-development.html#sharing-data-between-host-machine-and-container) between a host machine and a container using the `docker/mnt` directory.

-   {:.new}<!-- MAGECLOUD- 2575 -->**Configure with PHP constants**—Added support for [PHP constants]({{page.baseurl}}/cloud/project/magento-env-yaml.html#php-constants) in the `.magento.env.yaml` configuration file.

-   {:.new}<!--MAGECLOUD-2879-->**New Environment variable**—By default, only the Production environment has Google Analytics enabled. You can enable Google Analytics on the Staging and Integration environments using the  [ENABLE_GOOGLE_ANALYTICS environment variable]({{page.baseurl}}/cloud/env/variables-deploy.html#enable_google_analytics).

-   {:.fix}<!-- MAGECLOUD-2923 -->Fixed an issue that removed customized cron configurations from the `env.php` file after a redeployment. Now, custom cron configurations safely remain in the `env.php` file.

-   {:.fix}<!-- MAGECLOUD-2919 -->Fixed inconsistencies in the messages and [log levels]({{ page.baseurl }}/cloud/env/log-handlers.html#log-levels) for build, deploy, and post-deploy phases. Increased beginning and ending log message levels from **info** to **notice** for all phases and sub-phases. Added beginning and ending log messages, where appropriate.

-   {:.fix}<!-- MAGECLOUD-2862 -->Fixed an issue involving cron processes that prevented the start of the post-deploy phase, when configured. Now, if you have the post-deploy hook enabled, the cron processes are enabled again at the beginning of the post-deploy phase.

-   {:.fix}<!--MAGECLOUD-2736-->Resolved an issue that prevented a successful installation of Magento when specifying a custom database configuration. Previously, the installation process used the database configuration from the [MAGENTO_CLOUD_RELATIONSHIP variable]({{page.baseurl}}/cloud/env/variables-cloud.html) even if you designated customized connection information in the [DATABASE_CONFIGURATION environment variable]({{page.baseurl}}/cloud/env/variables-deploy.html#database_configuration).

-   {:.fix}<!--MAGECLOUD-2740-->Corrected the `config:dump` command so that it includes each website locale in the `system` section of the `config.local.php` file.

-   {:.fix}<!--MAGECLOUD-2797-->Fixed an issue that resulted in _warm-up_ errors during the post-deploy phase by correcting the source base URL reference.

-   {:.fix}<!--MAGECLOUD-2850-->Fixed an issue that generated files improperly during the `setup:di:compile` process, which affected the Amazon Pay module.

## v2002.0.14

-   {:.fix}<!--MAGECLOUD-2372-->**Verify Ideal State**—The `ideal-state` wizard now verifies the current configuration during each deployment and provides clear instructions for updating the configuration to achieve a faster, zero-downtime deployment.

-   {:.fix}<!--MAGECLOUD-2521-->**PCI Compliance**—Updated the messaging protocols for {{site.data.var.ece}} to require Transport Layer Security (TLS) version 1.2 when connecting with third-party messaging services. If you are using a message service that does not support TLS version 1.2, you must upgrade your service. Otherwise, the following error message displays when your {{site.data.var.ee}} application tries to connect to the message server to send an email: `Unable to connect via TLS`.

-   {:.new}<!--MAGECLOUD-2517-->**Deployment improvement**—Added validation to warn customers if a Staging or Production environment has `dev`, `debug`, or `debug_logging` options enabled to prevent performance issues caused by excessive logging activity.

-   {:.fix}**Deployment fixes**—

    -   <!--MAGECLOUD-2603-->Now maintenance mode is enabled at the start of the deploy phase and disabled at the end. If the deployment fails, the site remains in maintenance mode until the deployment issues are resolved.

    -   Reworked the deploy phase validation checks to downgrade the error level for the following deployment issues from `CRITICAL` to `WARNING` so that the deployment completes. Previously, these issues caused the deployment to fail.

       -  ADMIN_EMAIL is not set on upgrade.

       -  ADMIN_EMAIL or ADMIN_USERNAME is associated with another account.

       -  Environment configuration contains incorrect values for deploy or cloud variables.

       -  <!--MAGECLOUD-2600-->The Elasticsearch version on the cloud infrastructure is incompatible with the version of the elasticsearch/elasticsearch module supported by {{site.data.var.ece}}. See the [Elasticsearch troubleshooting article](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) in the Magento Support Knowledgebase.

-   {:.fix}<!--MAGECLOUD-2173-->Fixed an issue with the shared configuration settings in the `app/etc/config.php` file that caused `recursion detected` errors during deployment.

-   {:.fix}**Cron-related fixes**—

    -   <!--MAGECLOUD-2602-->Fixed a cron scheduling issue that prevented jobs from running if you specify a cron frequency other than the default (1 minute).

    -   <!--MAGECLOUD--2537-->Fixed an issue in the deploy phase that allowed cron jobs to continue running during deployment, which can cause database locks and other critical issues. Now, all cron jobs are stopped before the deploy phase begins and restarted after the deployment completes.

    -   <!--MAGECLOUD-2501-->Fixed the cron job workflow in versions 2.1.4 through 2.1.x to unlock frozen cron jobs so that they can be stopped before beginning deployment. Previously, a frozen cron job caused the deployment to stall.

-  {:.fix}<!--MAGECLOUD-2527-->Changed the format of the `config.php` file generated by the `vendor/bin/ece-tools config:dump` command to use short array syntax and 4-space indentation to comply with Magento coding standards.

-  {:.fix}<!--MAGECLOUD-2607-->Fixed a deployment error that occurs when the `.magento.env.yaml` contains `{{base_url}}` and `{{unsecure_base_url}}` placeholders for web configurations instead of the default URL configuration for a {{site.data.var.ece}} project.

## v2002.0.13

-   {:.new}<!--MAGECLOUD-2169-->**Enable zero-downtime deployment**—Now {{site.data.var.ece}} queues requests with required database changes during deployment and applies the changes as soon as the deployment completes. Requests can be held for up to 5 minutes to ensure that no sessions are lost. See [Static content deployment options to reduce deployment downtime on Cloud](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).

-   {:.new}**Docker Compose for Cloud**—Made the following improvements to the [Docker configuration]({{ page.baseurl }}/cloud/docker/docker-config.html) process:

    -   <!--MAGECLOUD-2359-->Added a command—`docker:config:convert` to convert PHP configuration files to Docker ENV format to simplify environment configuration. Now, you copy the PHP configuration files to the Docker directory and convert them to Docker ENV files. See [Launch Docker]({{ page.baseurl }}/cloud/docker/docker-config.html).

    -   <!--MAGECLOUD--2357-->The {{site.data.var.ece}} installation process now supports deploying to both read-only and read-write file systems to more closely emulate the Cloud file system. See [Configure Docker]({{ page.baseurl }}/cloud/docker/docker-config.html).

    -   <!--MAGECLOUD--2442-->Redis service support—Added a Redis image, which is deployed to a Docker container and configured automatically to work with your Docker installation.

    -   <!--MAGECLOUD--2358-->Varnish service support— Added a Varnish image, which is deployed automatically to a Docker container. After deployment, you can manually configure Varnish following Magento best practices. See [Configure and use Varnish]({{ page.baseurl }}/config-guide/varnish/config-varnish.html)

    -   <!--MAGECLOUD--2360-->Secure site access—Added SSL support to access your {{site.data.var.ee}} store and Admin panel.

-   {:.fix}<!--MAGECLOUD-2205-->**Improved {{site.data.var.ece}} extension support**—Downgraded the minimum version requirement for the guzzlehttp/guzzle package in the {{site.data.var.ece}} [composer.json file]({{ page.baseurl }}/cloud/reference/cloud-composer.html) to version 6.2 so that the `{{site.data.var.ct}}` package is compatible with more extensions.

-   {:.new}<!--MAGECLOUD-2363-->**Apply custom changes to your {{site.data.var.ee}} application during the build phase**—We split the build phase into two separate processes so that you can use hooks to apply custom changes to the generated static content before packaging the application for deployment. The *build:generate* process generates code, applies patches, and generates static content. The *build:transfer* process transfers the generated code and static content to the final destination. See [Application hooks]({{ page.baseurl }}/cloud/project/project-conf-files_magento-app.html#hooks).

-   {:.fix}**Environment configuration checks**—Improved validation of the environment configuration to warn customers about version incompatibilities and configuration errors before building and deploying {{site.data.var.ece}}.

    -   <!--MAGECLOUD-2183-->Added version-specific validation to identify unsupported or deprecated environment variables and values.

    -   <!--MAGECLOUD-2389-->Added an Elasticsearch compatibility check to warn users about Elasticsearch configuration issues. Now, the deployment fails if the version of Elasticsearch service on the server is incompatible with {{site.data.var.ee}}. Previously, the deployment succeeded even if the Elasticsearch version was incompatible, which caused product catalog issues after site deployment.

        You can resolve the incompatibility by [submitting a Support ticket]({{ page.baseurl }}/cloud/trouble/trouble.html) to upgrade Elasticsearch to a compatible version. For {{site.data.var.ee}} version 2.1.x and later, upgrade Elasticsearch to version 2.4. If you have Elasticsearch version 1.x or 2.x and do not want to upgrade, you can change the {{site.data.var.ee}} elasticsearch/elasticsearch requirement in composer.json to `elasticsearch/elasticsearch: "~2.0"`.

    -   <!--MAGECLOUD-2156-->Improved validation of environment variables to identify configuration settings that can cause conflicts during the build, deploy, and post-deploy phases. For example, a warning message displays during the install and upgrade process if the global setting for static content deployment conflicts with settings on the build or deploy phase.

-   {:.fix}**Environment variable updates**—Changed the following environment variables:

    -   <!--MAGECLOUD-2435-->**[SKIP_HTML_MINIFICATION global variable]({{ page.baseurl }}/cloud/env/variables-global.html#skip_html_minification)**—Changed the default value to `true` to enable on-demand HTML content minification, which minimizes downtime when deploying to Staging and Production environments. This configuration is required for zero-downtime deployments.

    -   <!--MAGECLOUD-1506-->**[CLEAN_STATIC_FILES deploy variable]({{ page.baseurl }}/cloud/env/variables-deploy.html#clean_static_files)**—Added the capability to manage the clean static files processing for static content generated during the build phase based on the CLEAN_STATIC_FILES environment variable setting. Previously, static content files generated during the build phase were always cleaned.

-   {:.new}**Logging**—Made the following changes to improve log messages and reduce log size:

    -   <!--MAGECLOUD-2489-->Deployment failure log entries now include the command output from the operations that cause the failures even if your environment configuration does not specify debug level logging. See [`MIN_LOGGING_LEVEL`]({{ page.baseurl }}/cloud/env/variables-global.html#min_logging_level).

    -   <!--MAGECLOUD-2209-->Added logging for deployment failures that occur when the generated factories required by some extensions cannot be generated correctly because the file system is in a read-only state.

    -   <!--MAGECLOUD-2402-->Reduced the deploy log size and fixed formatting issues caused by setup commands that use the interactive progress bar.

    -   <!--MAGECLOUD-2227-->Eliminated unnecessary verbosity and updated the priority levels for some log statements.

-   {:.fix}**Cron-specific fixes**—

    -   <!--MAGECLOUD-2427-->Changed the default cron job configuration settings for history lifetime from 3d (4320 min) to 1h (60 min) to prevent performance issues and deployment failures that can occur when the cron queue fills too quickly.

    -   <!--MAGECLOUD-2445-->Improved the cron job management process during the deploy phase to prevent database locks and other critical issues. Now, all cron jobs stop during the deploy phase and restart after deployment completes.

    -   <!--MAGECLOUD-2508-->Fixed an issue with the [`cron:unlock`]({{ site.baseurl }}/guides/v2.2/cloud/trouble/reset-cron-jobs.html) command so that it works in {{site.data.var.ee}} v2.1. Previously, the command was supported only in v2.1.

-   {:.fix}<!--MAGECLOUD-2491-->Fixed a Sitemap processing issue in the `{{site.data.var.ct}}` package that caused third-party extension conflicts after using the `{{site.data.var.ct}}` package to apply recent patches that included Sitemap-related changes.

-   {:.fix}<!-- MAGECLOUD-2182-->Fixed an issue with the [static content compression process]({{ page.baseurl }}/cloud/env/variables-deploy.html#scd_compression_level) process (`gzip`) that caused `not overwritten` and `no such file or directory` errors when referencing the compressed file during the deployment process.

-   {:.fix}<!--MAGECLOUD-2097-->Fixed permission checks that caused `Missing write permissions` errors during the upgrade process.

-   {:.fix}<!--MAGECLOUD-2444-->Fixed an issue that prevented the `php ./vendor/bin/ece-tools config:dump` command from removing redundant sections from the `config.local.php` file during the dump process if the store locale is not specified. Now you can easily move your configuration files between environments. After you update to `{{site.data.var.ct}}` v2002.0.13, regenerate older `config.local.php` files with the improved `config:dump` command. See [Configuration management for store settings]({{ page.baseurl }}/cloud/live/sens-data-over.html).

-   {:.fix}<!--MAGECLOUD-2556-->Fixed an issue that caused an error during the deploy phase if the route configuration in the `.magento/routes.yaml` file redirects from an [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) domain to a `www` domain.

-   {:.fix}<!--MAGECLOUD-2520-->Fixed an issue with the `_merge` option for the [`SEARCH_CONFIGURATION`]({{ page.baseurl }}/cloud/env/variables-deploy.html#search_configuration) variable that caused incorrect merge results if the updated `.magento.env.yaml` configuration file did not include the `engine` parameter value along with other updated values. Now, the merge operation correctly overwrites only the parameter values included in the updated `.magento.env.yaml` without requiring you to specify the `engine` parameter value.

-   {:.fix}<!-- MAGECLOUD-2515-->Fixed a Redis configuration issue that incorrectly enabled session locking for {{site.data.var.ece}} versions 2.1.11 and later, which can cause slow performance and timeouts. Now, session locking is disabled by default. The issue was caused by a change in the default behavior of the `disable_locking` parameter introduced in v1.3.4 of the Redis session handler package. See [colinmollenhour/php-redis-session-abstract package](https://github.com/colinmollenhour/php-redis-session-abstract).

## v2002.0.12

{:.bs-callout .bs-callout-info}
The`{{site.data.var.ct}}`version 2002.0.12 now supports Magento 2.1.14.

-   {:.new}<!-- MAGECLOUD-2250 -->**Docker Compose for Cloud**—Added a new command—`docker:build`—to generate a [Docker Compose]({{ page.baseurl }}/cloud/docker/docker-config.html) configuration from the Cloud `{{site.data.var.ct}}` repository.

-   {:.new}<!-- MAGECLOUD-2019 -->**Change Locales**—Now you can [change store locale]({{page.baseurl}}/cloud/live/sens-data-over.html#change-locales) without the exporting and importing configuration process. While Magento is in Production and the SCD_ON_DEMAND is enabled, the Magento store and admin locale options are available.

-   {:.new}<!-- MAGECLOU-1998 -->**Site map and Robots**—Created a [new workflow]({{ page.baseurl }}/cloud/trouble/robots-sitemap.html)to add a `robots.txt` file and generate a `sitemap.xml` file for a single domain configuration without requiring a change to the infrastructure.

-   {:.new}<!-- MAGECLOUD-1910 -->**Wizards**—Added two [new wizards]({{ page.baseurl }}/cloud/env/smart-wizards.html) to help you with Cloud configuration:

    -   `ideal-state`—configure the ideal state for minimal deployment downtime
    -   `master-slave`—configure load balancing for database and Redis

-   {:.new}<!-- MAGECLOUD-1521 -->**Module Refresh**—Added a new Cloud command—`module:refresh`—to enable modules that were disabled or not explicitly enabled, similar to the way that it is done automatically during a build. See [Build and deploy on local in Build phase]({{ page.baseurl }}/cloud/live/live-sanity-check.html#build).

-   {:.new}<!-- MAGECLOUD-2105 -->Added the ability to choose to merge or overwrite configuration for services using the `_merge` option in [CACHE]({{ page.baseurl }}/cloud/env/variables-deploy.html#cache_configuration), [SESSION]({{ page.baseurl }}/cloud/env/variables-deploy.html#session_configuration), [QUEUE]({{ page.baseurl }}/cloud/env/variables-deploy.html#queue_configuration), and [SEARCH]({{ page.baseurl }}/cloud/env/variables-deploy.html#search_configuration) configurations.

-   {:.new}<!-- MAGECLOUD-1908 -->**Environment Configuration sample file**—We added a `.magento.env.yaml` sample file to the `{{site.data.var.ct}}` package that includes a detailed description and possible values for each environment variable.

    -   <!-- MAGECLOUD-1907 -->We also added a deep validation for the `.magento.env.yaml` configuration that prevents failures in the deployment process caused by unexpected values. When a failure occurs, you now receive a detailed error message that begins with: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`

-   {:.new}Added the following [**Environment variables**]({{ page.baseurl }}/cloud/env/variables-intro.html):

    -   <!-- MAGECLOUD-1501 -->Now you can define multiple locales for each theme using the new [SCD_MATRIX]({{ page.baseurl }}/cloud/env/variables-deploy.html#scd_matrix) environment variable, which reduces the amount of theme files to deploy.

    -   <!-- MAGECLOUD-2047 --> Added the [DATABASE_CONFIGURATION]({{ page.baseurl }}/cloud/env/variables-deploy.html#database_configuration) environment variable to customize your database connections for deployment.
    -   <!-- MAGECLOUD-2129 -->The new [MIN_LOGGING_LEVEL]({{ page.baseurl }}/cloud/env/variables-global.html#min_logging_level) variable overrides the minimum logging level for all output streams without making changes to the code.

-   {:.fix}Fixed an issue that caused downtime between the deploy and post-deploy phase. Now, the post_deploy phase begins _immediately_ after the deploy phase ends.

-   {:.fix}<!-- MAGECLOUD-2268 -->Fixed an issue that did not clean the successful cron jobs, those with `status = success`, from the schedule.

-   {:.fix}<!-- MAGECLOUD-2113 -->Fixed an issue with the `post_deploy` hook that cleared the cache in the deploy phase instead of the post-deploy phase of the project.

-   {:.fix}<!-- MAGECLOUD-2034 -->Fixed an issue when using SCD with multiple locales, which generated the same `js-translation.json` file for each locale.

-   {:.fix}<!-- MAGECLOUD-2033  -->Optimized the `db:dump` command in the `{{site.data.var.ct}}` package to avoid locking tables and increase speed.

## v2002.0.11

{:.bs-callout .bs-callout-info}
The`{{site.data.var.ct}}`version 2002.0.11 now supports Magento 2.1.13.

-   {:.new}**Configuring read-only connections to non-master nodes**—This release adds the ability to configure a read-only connection to a non-master node to receive read-only traffic (for <!--MAGECLOUD-143 -->[Redis]({{ page.baseurl }}/cloud/env/variables-deploy.html#redis_use_slave_connection) and for <!--MAGECLOUD-143 --> [MariaDB]({{ page.baseurl }}/cloud/env/variables-deploy.html#mysql_use_slave_connection)).

-   {:.new}<!--MAGECLOUD-1910 -->**Configuration Wizard**—Added a new wizard to help verify your configuration for static content deployment. See [Smart wizards]({{ page.baseurl }}/cloud/env/smart-wizards.html).

-   {:.new}<!-- MAGECLOUD-1966-->**Symfony Console support**—Added support for Symfony Console 4 with Magento 2.3.

-   {:.fix}<!-- MAGECLOUD-1607 -->**Cron scheduling optimizations**—Improved the queue management and enhanced logging to help with debugging cron-related issues.

-   {:.fix}<!-- MAGECLOUD-1221 -->Deployment validation fails if an `ADMIN_EMAIL` or `ADMIN_USERNAME` value is the same as an existing Magento administrator account.

-   {:.fix}<!-- MAGECLOUD-1282 -->Removed SOLR support for 2.2.x versions. 2.1.x versions retain the ability to enable SOLR.

-   {:.fix}<!-- MAGECLOUD-1489 -->The first installation of the Staging & Production environments of a PRO project now includes different index prefixes for ElasticSearch to prevent possible conflicts while identifying records belonging to each environment.

-   {:.fix}<!-- MAGECLOUD-2021 -->Fixed an issue that interrupted the build phase for legacy architecture during static content deployment.

-   {:.fix}**Cron-specific Improvements**—<!-- MAGECLOUD-1607 -->Re-worked the cron implementation:

    -   Fixed an issue that caused the cron queue to fill quickly. Now it clears the outdated cron jobs in a more reliable way.

    -   Re-organized the sequence of cron jobs so that all jobs in separate threads launch prior to the general group.

    -   Improved logging to better assist in debugging cron issues.

    -   **NOTE**—This release addresses many cron-related issues. If you currently use some cron-related patches in _m2-hotfixes_, remove them.

-   {:.fix}**SCD-specific improvements**—

    -   <!-- MAGECLOUD-1819 -->You can now use the `VERBOSE_COMMANDS` and the `SCD_COMPRESSION_LEVEL` environment variables during both _build_ and _deploy_ phases.

    -   <!-- MAGECLOUD-2043 -->Fixed an issue that caused deployment to fail with a random error when encountering an unexpected value for the `SCD_COMPRESSION_LEVEL` environment variable. Improved the configuration validation to provide meaningful notifications. See [`SCD_COMPRESSION_LEVEL`]({{ page.baseurl }}/cloud/env/variables-build.html#scd_compression_level) for acceptable values.

    -   <!-- MAGECLOUD-2044 -->Fixed the behavior of the `SCD_COMPRESSION_LEVEL` environment variable configuration flow so the overrides work as expected.

    -   <!-- MAGECLOUD-2046 -->Fixed an issue that prevented the configuration of the `SCD_THREADS` environment variable in the `.magento.env.yaml` file _deploy_ stage.

## v2002.0.10

-   {:.new}<!-- MAGECLOUD-1285 -->**Static Content Deployment (SCD)**—There is a new, alternative deployment process to generate static content when requested (on-demand). This decreases downtime and improves cache handling by generating the most critical assets.

    -   <!-- MAGECLOUD-1738 -->**New environment variable**—Added the `SCD_ON_DEMAND` global environment variable to generate static content when requested.

    -   <!-- MAGECLOUD-1788 -->**Post-deploy hook**—Added a `post_deploy` hook for the `.magento.app.yaml` file that clears the cache and pre-loads (warms) the cache _after_ the container begins accepting connections. It is available only for Pro projects that contain [Staging and Production environments in the Project Web UI]({{ page.baseurl }}/cloud/trouble/pro-env-management.html) and for Starter projects. Although not required, this works in tandem with the `SCD_ON_DEMAND` environment variable.

-   {:.new}<!-- MAGECLOUD-1842 -->**Optimization**—Optimized moving or copying files during deployment to improve deployment speed and decrease loads on the file system.

-   {:.new}<!-- MAGECLOUD-1751 -->**Deployment Logging**—Added the ability to enable Syslog and Graylog Extended Log Format (GELF) handlers for outputting logs during the deployment process. See [Logging handlers]({{ page.baseurl }}/cloud/env/log-handlers.html).

-   {:.new}Added the following [**Environment variables**]({{ site.baseurl }}/guides/v2.2/cloud/env/variables-intro.html):

    -   <!-- MAGECLOUD-1556 -->`CRYPT_KEY`—Provide a cryptographic key to another environment when moving a database.

    -   <!-- MAGECLOUD-1621 and MAGECLOUD-1736-->`SKIP_HTML_MINIFICATION`—_Global_ environment variable that skips copying the static view files in the `var/view_preprocessed` directory and generates minified HTML when requested.

    -   <!-- MAGECLOUD-1738 -->`SCD_ON_DEMAND`—_Global_ environment variable to generate static content when requested.

    -    `WARM_UP_PAGES`—You can list the pages to use to pre-load the cache. Available in the new [Post-deploy variables]({{ site.baseurl }}/guides/v2.1/cloud/env/variables-post-deploy.html).

-   {:.fix}<!-- MAGECLOUD-982 -->We fixed an issue that involved a locally applied patch breaking the deployment on an instance. Now,`{{site.data.var.ct}}`can detect that a patch has been applied.

-   {:.fix}<!-- MAGECLOUD-1735 -->Fixed a conflict between JavaScript bundling and Gzip functionality. Now these features work correctly together.

-   {:.fix}<!-- MAGECLOUD-1744 -->Fixed an issue that caused c CLI commands to fail when using earlier PHP 7.0.x versions.

-   {:.fix}<!-- MAGECLOUD-1853 -->Fixed a Redis session locking issue that caused an Admin login delay. Also, the fix is available for 2.1.x.

## v2002.0.9

{:.bs-callout .bs-callout-info}
You must [upgrade the {{site.data.var.ece}} metapackage]({{ site.baseurl }}/guides/v2.1/cloud/project/project-upgrade-parent.html) to get this and all future updates.

#### New features

-   {:.new}<!-- MAGECLOUD-1086 -->**ece-tools**—The `{{site.data.var.ct}}` package now supports Magento 2.1.x. You must [upgrade to ece-tools]({{ site.baseurl }}/guides/v2.1/cloud/project/ece-tools-upgrade-project.html) to use these features.

-   {:.new}<!-- MAGECLOUD-1552 -->**Redis configuration**—You can now [configure Redis]({{ site.baseurl }}/guides/v2.1/cloud/env/variables-deploy.html#cache_configuration) page and default cache and Redis session storage using an environment variable.

-   {:.fix}<!-- MAGECLOUD-1437 -->**Search, AMQP, and Redis service improvements**—We unified the service configuration flow so that it now behaves the same way for all services. Manually editing the `env.php` file to configure services is no longer supported. You must use environment variables or the `.magento.env.yaml` file instead.

-   {:.fix}**Environment variables**—

    -    <!-- MAGECLOUD-1507 -->The use of `env:STATIC_CONTENT_THREADS` was deprecated and will be removed in a future release. Use the `STATIC_CONTENT_THREADS` environment variable instead.

    -    <!-- MAGECLOUD-1640 -->The `STATIC_CONTENT_EXCLUDE_THEMES` environment variable was deprecated. You must use the `SCD_EXCLUDE_THEMES` environment variable instead.

-   {:.fix}<!-- MAGECLOUD-1674 -->**Logging**—We simplified logging around built-in patching operations.

-   {:.fix}<!-- MAGECLOUD-1615 -->We removed `developer` mode support and the `APPLICATION_MODE` environment variable because they were causing unexpected behavior.

-   {:.fix}<!-- MAGECLOUD-1630 -->We fixed an issue that was causing static content deployment failures related to Redis. Now, multi-threaded static content deployment runs as designed.

-   {:.fix}<!-- MAGECLOUD-1175 -->We fixed an issue that was preventing users from saving modifications to configuration fields in the Admin, which are marked as sensitive after running the `app:config:dump` command.

-   {:.fix}<!-- MAGECLOUD-1674 -->We added support for an earlier version of `symfony/yaml` to fix conflicts with some packages, which are not yet compatible with the latest version.

## Older releases

See the [release notes archive]({{page.baseurl}}/cloud/release-notes/cloud-release-archive.html) for version 2002.0.8 and earlier.