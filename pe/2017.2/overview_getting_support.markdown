---
layout: default
title: "Getting support for Puppet Enterprise"
canonical: "/pe/latest/overview_getting_support.html"
---

{:.reference}
## Puppet Enterprise support life cycle

There are three phases of product support for each version of Puppet Enterprise: mainstream support, limited support, and end-of life (EOL).

| Phase              | Receives security updates and bug fixes? | Support response time                        | Help upgrading to a mainstream support version |
|--------------------|------------------------------------------|----------------------------------------------|---------------------------|
| Mainstream support | Yes                                      | SLA (service level agreement) response times | N/A                                                                          |
| Limited support    | No                                       | SLA response times                           | We'll support your upgrade with a variety of assistance and resource options |
| End-of-life (EOL)  | No                                       | "Commercially reasonable" assistance         | Contact support for assistance

{:.reference}
### Standard releases and long term support releases

We encourage you to upgrade to the [latest version](https://puppet.com/download-puppet-enterprise) or [latest long term support (LTS) version](https://puppet.com/misc/pe-files/previous-releases). If you want the latest features, install our latest **standard release**. If you prefer to retain the same version for an extended period, install our latest **long term support (LTS)** release.

| Type of release             | Release timeframe                  | In mainstream support                                      |
|-----------------------------|------------------------------------|---------------------|
| **Standard**                | Every six months (approximately) | Until the next standard or long term support (LTS) release |
| **Long term support (LTS)** | Every 18 months                    | 24 months after launch |                                              |

{:.reference}
### Supported Puppet Enterprise versions

We provide either **mainstream** or **limited support** for the versions of PE listed below. Puppet Enterprise 3.8 and earlier are now **end-of-life** (EOL).

PE versions     | Start mainstream support   | Start limited support      | EOL
----------------|--------------------------|--------------------------|---------
2017.2 | May 11, 2017                      | November 11, 207         | February 21, 2018
2017.1 | March 14, 2017                    | May 11, 2017            | February 21, 2018
2016.5 | December 13, 2016                 | March 14, 2017          | February 21, 2018
2016.4 (LTS) | October 20, 2016            | April 20, 2018           | October 21, 2018
2016.2 | June 21, 2016            | October 20, 2016            | February 21, 2018
2016.1 | April 7, 2016            | June 21, 2016               | February 21, 2018
2015.3 | December 8, 2015           | April 7, 2016             | February 21, 2018
2015.2 | July 28, 2015            | December 8, 2015            | February 21, 2018
3.8 | April 28, 2015            | December 31, 2016             | December 31, 2016

Also see the [operating system support life cycle](https://docs.puppet.com/pe/latest/sys_req_os.html#operating-system-support-life-cycles).

{:.concept}
### Open source tools and libraries

PE uses open source tools and libraries. We use both externally-maintained components (such as Ruby, Postgres, and the JVM) and projects which we own and maintain (such as Facter, Puppet Agent and Server, and PuppetDB.) Projects which we own and maintain are "upstream" of our commercial releases. Our open-source projects move faster and have shorter support life cycles than PE. We may discontinue updates to our open-source platform components before their commercial EOL dates. We vet upstream security and feature releases and update supported versions according to customer demand and our [Product Security Policy](/security/vulnerability_submission_process.html).

{:.concept}
## Getting support

Getting support for PE is easy; it is available from both Puppet, as a commercial support offering, and from our user community.

{:.section}
### Customer support portal

We provide responsive, dependable, quality support to resolve any issues regarding the installation, operation, and use of Puppet. There are two levels of [commercial support offerings for PE](http://puppet.com/support-services/customer-support): Standard and Premium. Both allow you to report your support issues to our confidential [customer support portal][portal]. When you purchase PE, you'll receive an account and log-on for the portal, which includes access to our [knowledge base][kb].

[kb]: https://support.puppet.com/hc/en-us
[portal]: https://support.puppet.com

**Customer support portal: [https://support.puppet.com][portal]**

{:.concept}
### PE support script

When seeking support, you might be asked to run an information-gathering support script. This script collects a large amount of system information, compresses it, and prints the location of the zipped tarball when it finishes running. Examine the collected data before forwarding it to our support team, it might contain sensitive information that you wish to redact.

The script is provided by the `pe_support_script` module bundled with the PE Installer. Running the command executes a single bash script which can be found at:
    `/opt/puppetlabs/puppet/cache/lib/puppet_x/puppetlabs/support_script/v1/puppet-enterprise-support.sh`

Run the support script on the command line of any PE node running RedHat, Ubuntu or SLES operating systems with the following command: `/opt/puppetlabs/bin/puppet enterprise support`.

{:.reference}
#### Information collected by the PE support script

The support script collects a large amount of system information that can help Puppet Support troubleshoot issues.

- iptables info: Is it loaded? What are the inbound and outbound rules for both IPv4 and IPv6?
- Facter output generated by `puppet facts find`
- SELinux status
- The amount of free disk and memory on the system
- hostname info: `/etc/hosts` and the output of `hostname --fqdn`
- List of established connections from `netstat`
- The output from `ifconfig`
- The umask of the system
- NTP configuration: what servers are available, the offset from them
- OS and kernel info from `uname -a` and `lsb_release -a` (if installed)
- The state of installed PE packages as reported by the system package manager
- a list of Ruby gems installed by `/opt/puppetlabs/puppet/bin/gem` and `/opt/puppetlabs/puppetserver/bin/gem`
- the current process list
- a listing of Puppet certs
- a listing of all services and their state (running/stopped, enabled/disabled, etc.)
- current environment variables
- whether the Puppet master is reachable
- the output of `mco ping` and `mco inventory`
- information about the `peadmin` user used to execute MCO commands:
  * the client configuration file at: `/var/lib/peadmin/.mcollective`
  * the client log  file at: `/var/lib/peadmin/.mcollective.d/client.log`
- the output of `ulimit -a` for the `pe-activemq` user along with a count of file descriptors used by the `pe-activemq` process
- a list of all Puppet modules on the system
- the output of `puppet module changes` (shows if any modules installed by PE have been modified)
- a listing (no content) of the files in
  * `/opt/puppetlabs`
  * `/var/log/puppetlabs`
  * `/var/opt/lib`
- reports the size of the PostgreSQL databases and relations
- PE PostgreSQL configuration from:
  - `/opt/puppetlabs/server/data/postgresql/9.4/data`
  - the output of `SELECT * FROM pg_settings;`
- The configuration used by PE RBAC to connect with a directory service, excluding sensitive information such as passwords
- r10k information:
  * configuration files
  * output of `r10k deploy display -p --detail`
- the output from [PE status API endpoints](./status_api.html)
- output from the PuppetDB [`/summary-stats` endpoint]({{puppetdb}}/api/admin/v1/summary-stats.html), which provides non-identifying database statistics for troubleshooting
- a list of active nodes from PuppetDB
- a list of active nodes from Orchestration Services
- a histogram of agent run start times from PuppetDB which is used to detect thundering herds
- output from the Puppet Server [`/environments` endpoint]({{puppet}}/http_api/http_environments.html), which lists available directory environments and module search paths
- the environment.conf and hiera.yaml configuration files from each environment

It also copies the following files:

- system logs
- the contents of `/etc/puppetlabs/` (being careful to avoid sensitive files, such as modules, manifests, ssl certs, and MCollective credentials)
- configuration files for PE services located under `/etc/sysconfig` or `/etc/default`  and `/etc/puppetlabs`.
- the contents of `/var/log/puppetlabs/`
- the contents of `/opt/puppetlabs/puppet/cache/state/`
- the contents of `/opt/puppetlabs/pe_metric_curl_cron_jobs`, if present
- the contents of `/etc/resolv.conf`
- the contents `/etc/nsswitch.conf`
- the contents of `/etc/hosts`

{:.concept}
### Join the Puppet Enterprise user group

<https://groups.google.com/a/puppet.com/forum/#!forum/pe-users>

- Click on “Sign in and apply for membership.”
- Click on “Enter your email address to access the document.”
- Enter your email address.

Your request to join will be sent to Puppet for authorization and you will receive an email when you’ve been added to the user group.

{:.concept}
### Getting support from the existing Puppet community

As a Puppet Enterprise customer you are more than welcome to participate in our large and helpful open source community as well as report issues against the open source project.

- Puppet open source user group:

    <http://groups.google.com/group/puppet-users>
- Puppet Developers group:

    <http://groups.google.com/group/puppet-dev>
- Report issues with the open source Puppet project:

    <https://tickets.puppetlabs.com/browse/PUP>