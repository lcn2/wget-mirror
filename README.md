# wget-mirror

Mirror a web site into a local directory


# To install

```sh
sudo make install
```


# Example

```sh
$ wget-mirror www.example.org http://www.example.org/index.html local_dir
```


# To use

```
/usr/local/bin/wget-mirror [-h] [-v] [-V] [-n] [-N] [-w wget] --
                           www.some.dom http://www.some.dom/URL local_dir [-flags ...]

    -h          print help message and exit
    -v level    set verbosity level (def level: 0)
    -V          print version string and exit

    -n          go thru the actions, but do not update any files (def: do the action)
    -N          do not process anything, just parse arguments (def: process something)

    -w wget	path to the wget tool (def: /opt/homebrew/bin/wget)

Exit codes:
     0         all OK
     1         some internal tool exited non-zero
     2         -h and help string printed or -V and version string printed
     3         command line error
     4	       unable to make or use local_dir
     5	       unable to find wget tool
 >= 10         internal error

Default wget flags used (override any of these by giving more flags end of the command line):

	-m	   ==>	--mirror		(same is: -r -N -l inf -nr)
	-U x	   ==>	--user-agent=x		(uses: wget-mirror-1.7.1)
	-nH	   ==>	--no-host-directories	(no www.host.org subdir)
	-np	   ==>	--no-parent		(don't upload above path)
	-D domlist ==>	--domains=domlist	(limit download to domains)
					(uses: --domains=__FIRST_ARG__)
	-t num	  ==>	--tries=num	(uses: 20, --tries=inf --> forever)
	-l num	  ==>	--level=num	(uses: 32, --level=inf --> infinite)
	--cache=off			(try to disable network caching)
	--passive-ftp			(passive FTP instead of active)

Useful additional wget -flags you may supply at the end of the command line:

	-q	  ==>	--quiet			(disable output)
	-o log	  ==>	--output-file=log	(output results to log)
	-a log	  ==>	--append-output=log	(append results to log)

	-R list	  ==>	--reject lest	(comma separated file and extensions)

	-Q quota  ==>   --quota=quota	(stop after download goes beyond quota)
	--limit-rate=20k		(to be nice to a site)
	--bind-address=host.or.ip	(bind to host.or.ip interface)
	--cache=on			(restore use of server side cache)

	-N	  ==>	--timestamping		(only mirror newer files)
	-nr	  ==>	--dont-remove-listing	(keep ftp .listing for mirrors)
	-r	  ==>	--recursive		(recursive download mirror)

	-L	  ==>	--relative		(follow only relative links)
	-p	  ==>	--page-requisites	(download all a page's files)
	-k	  ==>	--convert-links		(convert links for local view)
	-K	  ==>	--backup-converted	(keep orig version as .orig)
	--html-extension			(force .html suf on text/html)

NOTE:	Use --limit-rate=20k for 20k/sec rage limit
	    --limit-rate=inf for max (unlimited) rate (default is unlimited)
	Use --quiet to reduce output for something like a cron job
	Use --reject hitcount,.cgi to block download of .cgi's and hitcount
	Use --timestamping to not reload pages already on disk.  See: --mirror
	Use --dont-remove-listing so ftp mirroring works.	 See: --mirror
	Use --recursive to mirror links down to --level=num.	 See: --mirror
	Use --quota=5m to stop after 5 megabytes
	    --quota does not affect 1 file download, only recursive/multi ones
	Use --page-requisites so page has all files needed to display it
	Use --convert-links --backup-converted --html-extension for local view
	On multi-domain sites, comma separate all of them for the 1st arg
	    I.e.:, 1st arg could be: www.site.com,www.dmz.site.com
	Use of multiple --rejects is OK, the result is the union of rejects
	Use of multiple --domains=dom is OK, result is the union of domains
	Use of multiple --level=num is OK, the result is the last value
	Use of multiple --tries=num is OK, the result is the last value
	Use of multiple --cache={off,on} is OK, the result is the last value

wget-mirror version: 1.7.1 2025-03-23
```


# Reporting Security Issues

To report a security issue, please visit "[Reporting Security Issues](https://github.com/lcn2/wget-mirror/security/policy)".
