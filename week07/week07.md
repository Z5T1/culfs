                      Cucumber Linux from Scratch
                                Week 7
                            November 18, 2018

# Vulnerability Analysis and Patching Introduction

## What is a CVE?

In 1999, MITRE received a grant from the U.S. government to start the CVE
(Common Vulnerabilities and Exposures) project. This project aimed to assign a
unique ID to every security vulnerability in any product. 

These IDs are issued in the following format: CVE-2018-12345
* CVE - this part is always the literal letters "CVE" and serves to indicate
  that what follows is a CVE ID.
* 2018 - the year that the CVE ID was issued in.
* 12345 - a unique number within that year.
When these are combined together, it creates a unique ID for a vulnerability.

In addition to enumerating vulnerabilities, MITRE also maintains a database
with resources pertaining to each vulnerability. This database is known as the
MITRE CVE Dictionary is publicy accessible at https://cve.mitre.org/.

Additionally, NIST maintains the National Vulnerability Database (NVD) which is
syndicated by the MITRE CVE Dictionary; all of the information that is in the
MITRE CVE Dictionary is also in the NVD. In addition to this, the NVD
calculates the CVVS2 and CVVS3 severity ratings of each vulnerability and makes
them publicly available. The NVD is publicly accessible at
https://nvd.nist.gov/.

Here's an example of what the entry for CVE-2017-13721 looks like in each
database:
* MITRE: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-13721
* NVD: https://nvd.nist.gov/vuln/detail/CVE-2017-13721

### A (Brief) History of the CVE Project and why it is Necessary

Prior to this, each project would use its own vulnerability naming/numbering
scheme, which resulted in a single vulnerability having several different IDs
and names. This made it very difficult to keep it clear which vulnerability was
which, and which IDs were duplicates of what. Having one universal ID that
everyone could use to refer to one vulnerability eliminated this issue and made
the task of security patching substantially easier.

## How to Fix a Vulnerability

Generally, there are three ways you can fix a security vulnerability:
- Upgrade the affected package to a newer version that is not vulnerable.
- Apply the patch that fixes the vulnerability to your version of the package.
  This process is known as backporting.
- Make a configuration change so that the vulnerability is no longer
  exploitable.

Not every approach will work with every vulnerability, and some approaches work
better than others. This is just a guideline; every vulnerability must be
handled on a case by case basis.

# Vulnerability Patching Workshop

This week, we will be doing an interactive workshop instead of a follow along
lecture. For the workshop, we will analyze and patch the vulnerabilities in
this section. This will require recompiling several packages from source, so it
may be helpful to review the week02 content.

For all of these vulnerabilities, there is a complete analysis (along with the
solutions to these exercises) on the Cucumber Linux security tracker. I
encourage you to try fixing each vulnerability first without looking at the
Cucumber Linux Security Tracker, and look there only if you are stuck or want
to double check your work.

## CVE-2017-17087 (A Vulnerability in Vim)

This vulnerability can easily be fixed using all three approaches. I suggest
you fix it three times (once each way) in order to get a good understanding of
how each approach works, and what its strengths and weaknesses are.

This vulnerability is also very well documented, which will make your job much
easier. Sadly, this will not always be the case.

## CVE-2017-8817 (A Vulnerability in Curl)

This vulnerability does not have an easy proof of concept (PoC) available for
it. This makes it both less fun to analyze and harder to fix, but unfortunately
this happens a lot with vulnerabilities. Fortunately, this vulnerability is at
least well documented.

## CVE-2018-7169 (A Vulnerability in Shadow)

This vulnerability will be slightly more difficult to fix. As you will soon
find out, not every vulnerability has a nice analysis written for it and
sometimes you have to figure out the information about it yourself. I strongly
recommend fixing the other vulnerabilities first.

If you get stuck, here's a hint: the change in configuration approach will not
work here.

## Want More?

At this point, you should be beginning to feel comfortable with the process of
patching security vulnerabilities. If you want more practice, a good way to get
some is to pick vulnerabilities from the Cucumber Linux Security Tracker and
analyze them. Since I have already analyzed these vulnerabilities, I will be
able to help you if you get stuck or have questions.

# Resources

* MITRE CVE Dictionary: https://cve.mitre.org/
* National Vulnerability Database: https://nvd.nist.gov/
* Cucumber Linux Security Tracker: https://security.cucumberlinux.com/

The MITRE CVE Dictionary is the main place where all CVEs get logged. There is a page for each vulnerability, which contains links to other resources pertaining to that vulnerability. The National Vulnerability Database mirrors all of the information in the MITRE CVE Dictionary, but it also adds additional information not found on MITRE (such as the CVVS vulnerability severity score).

vi:syntax=markdown

