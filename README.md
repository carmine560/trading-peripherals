# trading-peripheral #

<!-- Python script that inserts Hyper SBI 2 maintenance schedules into Google
Calendar, exports its watchlists to Yahoo Finance, and extracts order status
-->

The `trading_peripheral.py` Python script can:

  * Retrieve [*SBI Securities Maintenance
    Schedules*](https://search.sbisec.co.jp/v2/popwin/info/home/pop6040_maintenance.html)
    and insert [Hyper SBI
    2](https://go.sbisec.co.jp/lp/lp_hyper_sbi2_211112.html) maintenance
    schedules into Google Calendar,
  * Replace watchlists on the SBI Securities website with Hyper SBI 2
    watchlists,
  * Export them from the `%APPDATA%\SBI
    Securities\HYPERSBI2\IDENTIFIER\portfolio.json` file to [*My
    Portfolio*](https://finance.yahoo.com/portfolios) on Yahoo Finance,
  * Extract the order status from the SBI Securities web page and copy it to
    the clipboard,
  * Take a snapshot of the `%APPDATA%\SBI Securities\HYPERSBI2` application
    data and restore it.

> **Warning**: This script is currently under heavy development.  Changes in
> functionality may occur at any time.

## Prerequisites ##

This script has been tested in [Python for
Windows](https://www.python.org/downloads/windows/) with Hyper SBI 2 and uses
the following web browser and packages:

  * [`google-api-python-client`](https://googleapis.github.io/google-api-python-client/docs/),
    [`google-auth-httplib2`](https://github.com/googleapis/google-auth-library-python-httplib2),
    and
    [`google-auth-oauthlib`](https://github.com/googleapis/google-auth-library-python-oauthlib)
    to access Google APIs
  * [Chrome](https://www.google.com/chrome/) to authenticate to the website and
    load the page
  * [`selenium`](https://www.selenium.dev/documentation/webdriver/) to drive a
    browser and
    [`webdriver-manager`](https://github.com/SergeyPirogov/webdriver_manager)
    to automatically update the driver
  * [`chardet`](https://github.com/chardet/chardet),
    [`pandas`](https://pandas.pydata.org/), and
    [`lxml`](https://lxml.de/index.html) to extract data from the web pages
  * [GnuPG](https://gnupg.org/index.html) and
    [`python-gnupg`](https://docs.red-dove.com/python-gnupg/) to encrypt and
    decrypt an application data archive
  * [`prompt_toolkit`](https://python-prompt-toolkit.readthedocs.io/en/master/index.html)
    to complete possible values or a previous value in configuring

Install each package as needed.  For example:

``` powershell
winget install Google.Chrome
winget install GnuPG.GnuPG
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt -U
```

## Usage ##

The `-m` and `-q` options use the Google Calendar and Gmail APIs.  Follow the
[*Google Calendar API
Quickstart*](https://developers.google.com/calendar/api/quickstart/python) and
[*Gmail API
Quickstart*](https://developers.google.com/gmail/api/quickstart/python) to
obtain a `client_secret_*.json` file.

If you use Chrome as your default web browser, create a separate profile that
stores your credentials.  Then, specify the profile directory as the value of
the `profile_directory` option, as shown below:

``` powershell
python trading_peripheral.py -G
```

The `-d` option encrypts a snapshot of the Hyper SBI 2 application data using
GnuPG.  By default, it uses the default key pair of GnuPG, but you can also
specify a key fingerprint as the value of the `fingerprint` option using the
`-G` option.

The `%LOCALAPPDATA%\trading-peripheral\trading_peripheral.ini` configuration
file stores these configurations.

### Options ###

  * `-P BROKERAGE PROCESS`: set the brokerage and the process [defaults: `SBI
    Securities` and `HYPERSBI2`]
  * `-m`: insert Hyper SBI 2 maintenance schedules into Google Calendar
  * `-s`: replace the watchlists on the SBI Securities website with the Hyper
    SBI 2 watchlists
  * `-y`: export the Hyper SBI 2 watchlists to My Portfolio on Yahoo Finance
  * `-q`: check the daily sales order quota in general margin trading for the
    specified Hyper SBI 2 watchlist and send a notification via Gmail if
    insufficient
  * `-o`: extract the order status from the SBI Securities web page and copy it
    to the clipboard
  * `-w`: backup the Hyper SBI 2 watchlists
  * `-d`: take a snapshot of the Hyper SBI 2 application data
  * `-D`: restore the Hyper SBI 2 application data from a snapshot
  * `-G`: configure general options and exit
  * `-M`: configure maintenance schedules and exit
  * `-Q`: configure checking the daily sales order quota and exit
  * `-O`: configure order status formats and exit
  * `-A`: configure actions and exit
  * `-C`: check configuration changes and exit

## Known Issues ##

  * Yahoo Finance does not appear to have stocks listed solely on the Nagoya
    Stock Exchange.
  * Extracting the order status assumes that you are day trading on margin.

## License ##

[MIT](LICENSE.md)

## Link ##

  * [*Python Scripting to Export Hyper SBI 2 Watchlists to Yahoo
    Finance*](https://carmine560.blogspot.com/2023/02/python-scripting-to-export-hyper-sbi-2.html):
    a blog post about serializing WebDriver commands
