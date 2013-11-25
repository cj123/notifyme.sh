# notifyme-sh

A simple shell tool to interact with [Prowl](http://www.prowlapp.com/) or [NotifyMyAndroid](https://www.notifymyandroid.com) using cURL and, if desired, sed to return information after the request is submitted.

## Installation

To install notifyme-sh on any Unix system, just clone this repository or download the .sh file to your system. Either create an alias to the file in your .profile or expose the script to your $PATH.

A Prowl API Key is needed to work with this script and can be retrieved after signing up on the [Prowl API Settings Page](https://www.prowlapp.com/api_settings.php) or [NotifyMyAndroid API Settings Page](https://www.notifymyandroid.com/account.jsp). In order for the script to see your API key, add a `PROWL_APIKEY` variable for prowl, or a `NMA_APIKEY` variable for NotifyMyAndroid to your environment in your .bash_profile or .profile file using

    export PROWL_APIKEY="key"
    export NMA_APIKEY="key"

If the script does not find the API key variable, the script will abort and you will be prompted to resolve the issue.

## Options

### Required

- S (Service)
  - either `prowl` or `nma`
- a (Application)
  - This option sets which application the message is coming from like a torrent application or even another shell script.
  - If there are multiple words, they must be wrapped in quotes
- s (Subject)
  - This option sets the subject of the message such as "Download Complete" or "Backup Complete".
  - If there are multiple words, they must be wrapped in quotes
- Message
  - The main message of the request is the remainder of the input after the options. This can be quoted or left unquoted.

### Optional

- p (Priority)
  - Allows you to change the priority of the message (for example to break through ProwlApp's "quiet mode")
  - Value from -2 (Very Low) to 2 (Emergency)
  - Default is 0 (Standard message)
- v (Verbose)
  - If this flag is included and sed is installed on the computer, the response will be processed from Prowl and a success or failure message will be displayed.
  - If sed isn't found the verbose output will be aborted.
- r (Raw)
  - This flag will display the raw XML output returned from Prowl. This is useful when trying to debug a situation as not all possible error messages have been setup in verbose mode.


## Example Input

    ./notifyme.sh -S prowl -s Subject -a Application The rest of the string is the main message

    ./notifyme.sh -S prowl -s Subject -a Application -p 2 "This is a very high priority message"

    ./notifyme.sh -S nma -s "Sample Subject" -a "Sample Application" "This example uses quotes to better segment off which strings belong to which section"

## Output

By default no output is generated by this script as in the majority of cases, this script will be run in the background or called from other scripts. In these cases, output from other scripts can often cause problems. If however the result is needed to be known, use the verbose or raw flags to see if the call was successful or not.
