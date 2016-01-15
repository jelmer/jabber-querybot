# Introduction

This is jabber-querybot - a modular perl jabber bot

jabber-querybot connects a jabber account and wait for messages. If a message
comes in, it forward it to your self programmend modul. The return string of
your module, jabber-querybot send it back to the jabber sender.

It is designed to be re-usable and to make it easy to write small
Jabber bots that do one thing and do it well. A simple concept with a
lot of examples and experiences are implemented.

Check this site for the latest version of this software:

<http://github.com/micressor/jabber-querybot>

jabber-querybot is available in debian:

	apt-get install jabber-querybot

For more info, please read the manpage file.

# Instructions

1. Create a jabber account on a jabber-server around

2. Create a bot application:

	cd examples
	cp Querymodule.pm /etc/jabber-querybot/Mybot.pm
	cd /etc/jabber-querybot
	ln -s Mybot.pm Querymodule.pm

Modify login parameters to your jabber-bot-account

	vi Mybot.pm
	our $hostname	       = "swissjabber.ch";
	our $user            = "";
	our $password        = "";
	our $ident           = "Testbot";
	our $bot_admin       = "\@swissjabber.ch";
	our $port            = "5222";
	our $timeout         = "5";
	our $service_name    = "$user\@$hostname";
	our $bot_description = "Bot help title Bot description";

For each jabber message, jabber-querybot will execute sub run_query,
that you can write here your application.

You can control how your jabber response will be:

* error = error message stanza
* presence = error as presence stanza
* ignore = ignore message

# Options

jabber-querybot has a lot of variables which you can easy modify for
what you need:

## querystatus

$querystatus = [ 0 | 1 ]

* 0 = Bot will not proceed any incoming jabber messages.
* 1 = Bot will proceed incoming messages.

## penalty_status

If the bot has too much workload, it goes to penalty status and wait some
time until his status change back to normal.

$timer_reconnect_default = 21600

Every 21600 seconds (6 hours) the bot will shutdown automatically, wait 10
seconds and starting up again.

$timer_auto_query = 0

If you set in your module this variable to 60, the bot will every 60 seconds
call the function run_auto_query() which you may use for several things.

## System load

If your systems load is >=6, this bot will shutdown the jabber connection
and check every 10 seconds systems load. If load <=2, bot will start over.

# License

jabber-querybot is free software, available under the [GNU General Public License, Version 3](http://www.gnu.org/licenses/gpl.html).
