# trading-peripheral #

<!-- Python script that exports Hyper SBI 2 watchlists to Yahoo Finance,
extracts order status, and inserts maintenance schedules into Google Calendar
-->

<!-- hypersbi2 python chrome selenium webdrivermanager pandas google-api gnupg
-->

A `trading_peripheral.py` Python script:

  * replaces watchlists on the SBI Securities website with [Hyper SBI
    2](https://go.sbisec.co.jp/lp/lp_hyper_sbi2_211112.html) watchlists
  * exports them from the `%APPDATA%\SBI
    Securities\HYPERSBI2\IDENTIFIER\portfolio.json` file to [*My
    Portfolio*](https://finance.yahoo.com/portfolios) on Yahoo Finance
  * extracts order status from the SBI Securities web page and copies them to
    the clipboard
  * retrieves [*SBI Securities Maintenance
    Schedules*](https://search.sbisec.co.jp/v2/popwin/info/home/pop6040_maintenance.html)
    and inserts them into Google Calendar
  * takes a snapshot of the `%APPDATA%\SBI Securities\HYPERSBI2` application
    data and restores it

> **Warning** This script is currently under heavy development.  Changes in
> functionality can occur at any time.

## Prerequisites ##

This script has been tested in [Python for
Windows](https://www.python.org/downloads/windows/) with Hyper SBI 2 and uses
the following web browser and packages:

  * [Chrome](https://www.google.com/chrome/) to authenticate to the website and
    load the page
  * [Selenium WebDriver](https://www.selenium.dev/documentation/webdriver/) to
    drive a browser
  * [WebDriver Manager for
    Python](https://github.com/SergeyPirogov/webdriver_manager) to
    automatically update the driver
  * [pandas](https://pandas.pydata.org/) to extract data from the web pages
  * [google-api-python-client](https://googleapis.github.io/google-api-python-client/docs/),
    [google-auth-httplib2](https://github.com/googleapis/google-auth-library-python-httplib2),
    and
    [google-auth-oauthlib](https://github.com/googleapis/google-auth-library-python-oauthlib)
    to access Google APIs
  * [GnuPG](https://gnupg.org/index.html) and
    [python-gnupg](https://docs.red-dove.com/python-gnupg/) to encrypt and
    decrypt application data archive
  * (optional)
    [prompt_toolkit](https://python-prompt-toolkit.readthedocs.io/en/master/index.html)
    to complete possible values or a previous value in configuring

Install each package as needed.  For example:

``` powershell
winget install Google.Chrome
pip install selenium
pip install webdriver-manager
pip install pandas
pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
winget install GnuPG.GnuPG
pip install python-gnupg
pip install prompt_toolkit
```

## Usage ##

If you are using Chrome as your default web browser, create a separate profile
that stores your credentials and specify it as the value of the
`profile_directory` option as follows:

``` powershell
py trading_peripheral.py -G
```

A `%LOCALAPPDATA%\trading-peripheral\trading_peripheral.ini` configuration file
stores these configurations.

### Options ###

| Option                 | Description                                                                            | Chrome   | pandas   | Google API | GnuPG    |
|------------------------|----------------------------------------------------------------------------------------|----------|----------|------------|----------|
| `-P BROKERAGE PROCESS` | set the brokerage and the process [defaults: `SBI Securities` and `HYPERSBI2`]         |          |          |            |          |
| `-w`                   | backup the Hyper SBI 2 watchlists                                                      |          |          |            |          |
| `-s`                   | replace the watchlists on the SBI Securities website with the Hyper SBI 2 watchlists   | required |          |            |          |
| `-y`                   | export the Hyper SBI 2 watchlists to My Portfolio on Yahoo Finance                     | required |          |            |          |
| `-o`                   | extract the order status from the SBI Securities web page and copy it to the clipboard | required | required |            |          |
| `-m`                   | insert maintenance schedules into Google Calendar                                      |          | required | required   |          |
| `-d`                   | take a snapshot of the Hyper SBI 2 application data                                    |          |          |            | required |
| `-D`                   | restore the Hyper SBI 2 application data from a snapshot                               |          |          |            | required |
| `-G`                   | configure general options and exit                                                     |          |          |            |          |
| `-O`                   | configure order state formats and exit                                                 |          |          |            |          |
| `-M`                   | configure maintenance schedules and exit                                               |          |          |            |          |
| `-A`                   | configure actions and exit                                                             |          |          |            |          |

## Known Issues ##

  * Yahoo Finance does not seem to have stocks listed solely on the Nagoya
    Stock Exchange.
  * Extracting order status assumes day trading on margin.

## License ##

[MIT](LICENSE.md)

## Link ##

  * [*Python Scripting to Export Hyper SBI 2 Watchlists to Yahoo
    Finance*](https://carmine560.blogspot.com/2023/02/python-scripting-to-export-hyper-sbi-2.html):
    a blog post about serializing WebDriver commands
