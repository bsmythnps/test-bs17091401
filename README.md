# REDIRECTS AND VANITY URLS

As managed through the rewrites.yml file.

Note that some redirects are managed through Fastly, but these are mostly domain-level redirects.

## What's the difference?

* **Redirect:** A rule telling the web browser to send visitors from one URL to another with a [301 redirect](https://blog.hubspot.com/blog/tabid/6307/bid/7430/what-is-a-301-redirect-and-why-should-you-care.aspx)
* **Vanity URL (vURL) - tracked:** A user-friendly redirect, usually short and easily typed. These include a Google utm tracking code if they're part of a campaign
* **Vanity URL (vURL) - untracked** As above, but without a tracking code. Essentially a short redirect

## How rewrites.yml works

* One line = one rule
* Two types of rule:
	* One-to-one
		* Affect one specific page
		* e.g. _\- \[\'\/source\/url\', \'\\\/destination\\\/url\'\]_
	* Regular expression
		* Affect multiple pages
		* e.g. _- \[\!ruby\/regexp \'\/\\\/source\\\/directory\/i\', \'\\\/destination\\\/url\'\]_
* Whenever someone requests a URL from the website, the server:
	1. Reads rewrites.yml, starting from the _top_ of the file
	2. Finds the the _first_ rule with a source URL that matches the requested URL
	3. Reads rewrites.yml again, using the destination URL of the matching rule
* When the requested URL can't be found in redirects.yml, the server delivers that page
* So the order of the rule in rewrites.yml is important
* In general:
	* One-to-one rules (more specific) should be towards the top of the file
	* Regex rules (more general) at the bottom
* vURLs are defined towards the top of the file (around line 60) for easy access
	* Use standardised campaign tag: ?utm_medium=vanity-url&utm_source=00-00-00&utm_campaign=[vURL path]
	* Note: The vURL tagging method needs to change soon to fit better with reporting requirements

## Redirect update process

### For content authors and editors: updates twice a week

* For now we’ll use the same twice-weekly process we had before migration.
* Deadlines to send reqs to Digital are:
	* 3pm Mon (deployed COB Tue)
	* 3pm Wed (deployed COB Thu)

### For Digital team

\(Draft\)

1. Author/editor sends request to Digital
2. Digital checks request, updates rewrites.yml in Github
3. Before COB Mon or Wed, Digital requests deployment of new config
4. On Tue or Thu, Ops checks file syntax, deploys update, notifies Digital
5. Digital tests redirects

_Note:_ For bulk or regex redirects it may be wise to check on UAT first.

## vURL update process

\(Draft\)
* vURLs are more complex because they affect reporting and user tracking.
* They are implemented the same way as above, but should be planned alongside content and promotion

## Tools

\(Draft\)

* [Bulk redirect generator](https://docs.google.com/spreadsheets/d/1oJbR6pUwr4dCyYK4QK8ZZm_kMzdHUAN8s3CoAx1WgzQ/edit#gid=0)
* Editors \(with YML syntax\)
	* Sublimetext3
	* Atom
* [YAMLlint syntax checker](http://www.yamllint.com) \(tends to time out\)

## Github config

\(Draft\)

* Repo: [NPS Website Redirects](https://github.com/NPSMedicineWise/nps-website-redirects)

## Issues and to-do

* Do we use JIRA to request Ops deployment?
* Get git working
