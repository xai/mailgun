# xmailgun
Send bulk mail using configs and templates.

I use this tool to e.g., send invitations to conferences or deploy surveys.

## Install
```
go install github.com/xai/xmailgun@latest
```

## Usage
```
Usage of xmailgun:
  -config string
    	configuration file for smtp connection (json)
  -dryrun
    	do not actually send mails
  -task string
    	task file (json)
```

Start by looking at the configuration files in `./examples/`.

The core configuration items are:
* An `smtp config` is a json file that stores everything that is needed for contacting the smtp server. Do not commit this file to a repository.
* A `task file` is a json file that specifies variables, such as sender and subject, that are applied to *all* mails. It also specifies the file path to the mail body template and the recipient file.
* A `mailbody template` is a text file that may contain markers that can be replaced by xmailgun.
* A `recipients list` is a json file that contains variables specific to each recipient. You can, e.g., provide specific substitutions of markers and recipient-specific attachments in this file.

## Disclaimer
Please be aware that sending broken/incomplete or even correct and complete mails to a large number of recipients is a good way to make a huge number of people angry at you.

This tool is provided "as is" without warranty of any kind.  
If it damages anything or causes trouble, this is entirely your problem.  
Also, do not abuse this tool for spamming!

You can specify `-dryrun` to print the mails to stdout instead of handing them to the specified smtp server.  
If you do not specify `-dryrun`, a safety countdown is started to give you the chance of cancelling the bulk mailing.  
After sending a bunch of mails, the tool will automatically enter a cooldown phase to give the smtp server time to recover and to avoid triggering spam prevention measurements.

## A note to avoid potential confusion due to my tool's name
Please not that `xmailgun` is **not** affiliated in any way with the company "mailgun" or their service.

`xmailgun` is a standalone tool that I just happened to name in a similar way due to its mass mailing functionality.
It creates and issues SMTP requests locally without using any external services.