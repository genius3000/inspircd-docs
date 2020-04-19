---
title: v3 Modes
---

## InspIRCd Modes

InspIRCd supports five types of mode:

Type      | Parameter when adding?       | Parameter when removing?     | Can be set multiple times?                                        | Description
--------- | ---------------------------- | ---------------------------- | ----------------------------------------------------------------- | -----------
Switch    | No                           | No                           | No                                                                | Toggles the behaviour of a feature on a channel or user.
Parameter | Yes                          | No                           | No                                                                | Enables and configures the behaviour of a feature on a channel or user.
ParamBoth | Yes                          | Yes                          | No                                                                | The same as a Parameter mode only the parameter must be specified to remove it.
Prefix    | Yes; channel member nickname | Yes; channel member nickname | Yes; once per channel member                                      | Grants/revokes a status rank to the user specified in the parameter.
List      | Yes                          | Yes                          | Yes; up to the [maximum list size](/3/configuration/#ltmaxlistgt) | Adds/removes entries from a list.

### Core Channel Modes

Name       | Character | Type      | Parameter Syntax | Usable By         | Description
---------- | --------- | --------- | ---------------- | ----------------- | -----------
ban        | b         | List      | `<mask>`         | Channel operators | Bans users matching &lt;mask&gt; from joining the channel.
inviteonly | i         | Switch    | *None*           | Channel operators | Prevents users from joining the channel without an invite.
key        | k         | ParamBoth | `<key>`          | Channel operators | Prevents users from joining the channel who have not specified the &lt;key&gt; password.
limit      | l         | Parameter | `<count>`        | Channel operators | Allows no more than &lt;count&gt; users to join the channel.
moderated  | m         | Switch    | *None*           | Channel operators | Prevents users without a prefix rank from messaging the channel.
noextmsg   | n         | Switch    | *None*           | Channel operators | Prevents users who are not in the channel from messaging the channel.
op         | o         | Prefix    | `<nick>`         | Channel operators | Grants channel operator status to &lt;nick&gt;.
private    | p         | Switch    | *None*           | Channel operators | Hides the channel in `/WHOIS` from people who are not a member. You probably want the `s` (secret) channel mode rather than this.
secret     | s         | Switch    | *None*           | Channel operators | Hides the channel in `/WHOIS` and `/LIST` from people who are not a member.
topiclock  | t         | Switch    | *None*           | Channel operators | Prevents non-channel operators from changing the channel topic.
voice      | v         | Prefix    | `<nick>`         | Channel operators | Grants channel voice status to &lt;nick&gt;.

#### Example Usage

Bans users matching `*!*@example.com` from joining \#channel:

```plaintext
/MODE #channel +b *!*@example.com
```

Sets the channel key for \#cheese to "cheddar":

```plaintext
/MODE #channel +k cheddar
```

Removes the channel key for \#cheese:

```plaintext
/MODE #channel -k cheddar
```

Limits \#channel to 100 users:

```plaintext
/MODE #channel +l 100
```

Grants channel operator status to Sadie in \#channel:

```plaintext
/MODE #channel +o Sadie
```

Removes channel operator status from Sadie in \#channel:

```plaintext
/MODE #channel -o Sadie
```

Grants channel voice status to Sadie in \#channel:

```plaintext
/MODE #channel +v Sadie
```

Removes channel voice status from Sadie in \#channel:

```plaintext
/MODE #channel -v Sadie
```

### Modular Channel Modes

For more details and examples of the channel modes of a specific module please refer to [the appropriate page for that module](/3/modules).

<!-- begin module channel modes -->
Name          | Character | Type      | Paramter Syntax                                 | Usable By                           | Description                                                                                                                                                                                                   | Provided By
--------------|-----------|-----------|-------------------------------------------------|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------
blockcolor    | c         | Switch    | *None*                                          | Channel operators                   | Enables blocking messages that contain IRC formatting codes.                                                                                                                                                  | [blockcolor](/3/modules/blockcolor)
delaymsg      | d         | Parameter | `<seconds>`                                     | Channel operators                   | Prevents newly joined users from speaking until &lt;seconds&gt; seconds have passed.                                                                                                                          | [delaymsg](/3/modules/delaymsg)
banexception  | e         | List      | `<mask>`                                        | Channel operators                   | Exempts users matching &lt;mask&gt; from the `b` (ban) channel mode.                                                                                                                                          | [banexception](/3/modules/banexception)
flood         | f         | Parameter | `(*)<lines>:<seconds>`                          | Channel operators                   | Kicks users who send more than &lt;lines&gt; messages in the last &lt;seconds&gt; seconds. If prefixed with * then offending users are also banned.                                                           | [messageflood](/3/modules/messageflood)
filter        | g         | List      | `<glob>`                                        | Channel operators                   | Prevents users from sending messages that match &lt;glob&gt;.                                                                                                                                                 | [chanfilter](/3/modules/chanfilter)
joinflood     | j         | Parameter | `<joins>:<seconds>`                             | Channel operators                   | Prevents more than &lt;joins&gt; joins in the last &lt;seconds&gt; seconds.                                                                                                                                   | [joinflood](/3/modules/joinflood)
c_registered  | r         | Switch    | *None*                                          | Channel operators                   | Marks the channel as being registered.                                                                                                                                                                        | [services_account](/3/modules/services_account)
auditorium    | u         | Switch    | *None*                                          | Channel operators                   | Enables auditorium mode.                                                                                                                                                                                      | [auditorium](/3/modules/auditorium)
autoop        | w         | List      | `<status>:<mask>`                               | Channel operators                   | Grants the &lt;status&gt; rank to users matching &lt;mask&gt; on join.                                                                                                                                        | [autoop](/3/modules/autoop)
operprefix    | y         | Prefix    | `<nick>`                                        | Server operators                    | Grants channel operprefix status to &lt;nick&gt;.                                                                                                                                                             | [operprefix](/3/modules/operprefix)
sslonly       | z         | Switch    | *None*                                          | Channel operators                   | Prevents users who are not connected using TLS (SSL) from joining the channel.                                                                                                                                | [sslmodes](/3/modules/sslmodes)
allowinvite   | A         | Switch    | *None*                                          | Channel operators                   | Allows unprivileged users to use the `/INVITE` command.                                                                                                                                                       | [allowinvite](/3/modules/allowinvite)
blockcaps     | B         | Switch    | *None*                                          | Channel operators                   | Enables blocking excessively capitalised messages.                                                                                                                                                            | [blockcaps](/3/modules/blockcaps)
noctcp        | C         | Switch    | *None*                                          | Channel operators                   | Enables blocking channel messages that contain CTCPs.                                                                                                                                                         | [noctcp](/3/modules/noctcp)
delayjoin     | D         | Switch    | *None*                                          | Channel operators                   | Prevents users from receiving JOIN messages until the joining user speaks.                                                                                                                                    | [delayjoin](/3/modules/delayjoin)
repeat        | E         | Parameter | `[~ *]<lines>:<sec>[:<difference>][:<backlog>]` | Channel operators                   | Configures the messages that should be considered a repeat. If prefixed with ~ the messages are blocked. If prefixed with * then offending users are banned. If not prefixed then offending users are kicked. | [repeat](/3/modules/repeat)
nickflood     | F         | Parameter | `<changes>:<seconds>`                           | Channel operators                   | Prevents more than &lt;changes&gt; nickname changes in the last &lt;seconds&gt; seconds.                                                                                                                      | [nickflood](/3/modules/nickflood)
censor        | G         | Switch    | *None*                                          | Channel operators                   | Enables censoring messages sent to the channel.                                                                                                                                                               | [censor](/3/modules/censor)
history       | H         | Parameter | `<count>:<period>`                              | Channel operators                   | Sends up to &lt;count&gt; messages from the last &lt;period&gt; on join.                                                                                                                                      | [chanhistory](/3/modules/chanhistory)
invex         | I         | List      | `<mask>`                                        | Channel operators                   | Exempts users matching &lt;mask&gt; from the `i` (inviteonly) channel mode.                                                                                                                                   | [inviteexception](/3/modules/inviteexception)
kicknorejoin  | J         | Parameter | `<seconds>`                                     | Channel operators                   | Prevents who have been kicked from rejoining until &lt;seconds&gt; seconds have passed.                                                                                                                       | [kicknorejoin](/3/modules/kicknorejoin)
noknock       | K         | Switch    | *None*                                          | Channel operators                   | Disables the usage of the `/KNOCK` command on this channel.                                                                                                                                                   | [knock](/3/modules/knock)
redirect      | L         | Parameter | `<channel>`                                     | Channel operators                   | Redirects all new users to &lt;channel&gt; when the user limit is reached.                                                                                                                                    | [redirect](/3/modules/redirect)
regmoderated  | M         | Switch    | *None*                                          | Channel operators                   | Prevents users who are not logged into a services account from speaking in the channel.                                                                                                                       | [services_account](/3/modules/services_account)
nonick        | N         | Switch    | *None*                                          | Channel operators                   | Prevents users from changing their nickname whilst in the channel.                                                                                                                                            | [nonicks](/3/modules/nonicks)
operonly      | O         | Switch    | *None*                                          | Server operators                    | Prevents non-server operators from joining the channel.                                                                                                                                                       | [operchans](/3/modules/operchans)
permanent     | P         | Switch    | *None*                                          | Server operators                    | Prevents the channel from being deleted when the last user leaves.                                                                                                                                            | [permchannels](/3/modules/permchannels)
nokick        | Q         | Switch    | *None*                                          | Channel operators                   | Prevents privileged users from using the `/KICK` command.                                                                                                                                                     | [nokicks](/3/modules/nokicks)
reginvite     | R         | Switch    | *None*                                          | Channel operators                   | Prevents users who are not logged into a services account from joining the channel.                                                                                                                           | [services_account](/3/modules/services_account)
stripcolor    | S         | Switch    | *None*                                          | Channel operators                   | Enables stripping of IRC formatting codes from channel messages.                                                                                                                                              | [stripcolor](/3/modules/stripcolor)
nonotice      | T         | Switch    | *None*                                          | Channel operators                   | Enables blocking messages sent with the `/NOTICE` command.                                                                                                                                                    | [nonotice](/3/modules/nonotice)
exemptchanops | X         | List      | `<restriction>:<mode>`                          | Channel operators                   | Exempts users with the &lt;mode&gt; prefix mode or higher from &lt;restriction&gt;.                                                                                                                           | [exemptchanops](/3/modules/exemptchanops)
join          | Y         | Prefix    | `<nick>`                                        | Server operators                    | Grants channel official-join status to &lt;nick&gt;.                                                                                                                                                          | [ojoin](/3/modules/ojoin)
namebase      | Z         | List      | `<name>[=<value>]`                              | Depends on the mode in &lt;name&gt; | Allows users to add, remove, and view the modes of a specific target.                                                                                                                                         | [namedmodes](/3/modules/namedmodes)
<!-- end module channel modes -->

### Core User Modes

Name      | Character | Type      | Parameter Syntax  | Usable By        | Description
--------- | --------- | --------- | ----------------- | ---------------- | -----------
invisible | i         | Switch    | *None*            | Anyone           | Marks the user as invisible.
oper      | o         | Switch    | *None*            | Server operators | Marks the user as a server operator (can only be set by the server).
snomask   | s         | Parameter | `(+|-)<snomasks>` | Server operators | Enables receiving the specified types of [server operator notice](/3/snomasks).
wallops   | w         | Switch    | *None*            | Anyone           | Enables receiving `/WALLOPS` messages from server operators.

#### Example Usage

Enables snomasks `l` (LINK) and `L` (REMOTELINK) and disables snomask `d` (DEBUG):

```plaintext
/MODE YourNick +s +lL-d
```

Enables all available snomasks:

```plaintext
/MODE YourNick +s +*
```

Disables all enabled snomasks:

```plaintext
/MODE YourNick -s
```

### Modular User Modes

For more details and examples of the user modes of a specific module please refer to [the appropriate page for that module](/3/modules).

<!-- begin module user modes -->
Name            | Character | Type   | Paramter Syntax | Usable By                              | Description                                                                                         | Provided By
----------------|-----------|--------|-----------------|----------------------------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------------
deaf_commonchan | c         | Switch | *None*          | Anyone                                 | Requires other users to have a common channel before they can message this user.                    | [commonchans](/3/modules/commonchans)
deaf            | d         | Switch | *None*          | Anyone                                 | Prevents the user from receiving channel messages.                                                  | [deaf](/3/modules/deaf)
callerid        | g         | Switch | *None*          | Anyone                                 | Enables whitelisting of who can message the user.                                                   | [callerid](/3/modules/callerid)
helpop          | h         | Switch | *None*          | Server operators                       | Marks the user as being available for help.                                                         | [helpop](/3/modules/helpop)
servprotect     | k         | Switch | *None*          | Servers                                | Protects services pseudoclients against kicks, kills, and channel prefix mode changes.              | [servprotect](/3/modules/servprotect)
u_registered    | r         | Switch | *None*          | Anyone                                 | Marks the user as being logged into a services account.                                             | [services_account](/3/modules/services_account)
cloak           | x         | Switch | *None*          | Anyone                                 | Enables hiding of the user's hostname.                                                              | [cloaking](/3/modules/cloaking)
sslqueries      | z         | Switch | *None*          | Anyone                                 | Prevents messages from being sent to or received from a user that is not connected using TLS (SSL). | [sslmodes](/3/modules/sslmodes)
bot             | B         | Switch | *None*          | Anyone                                 | Marks the user as a bot.                                                                            | [botmode](/3/modules/botmode)
privdeaf        | D         | Switch | *None*          | Anyone                                 | Prevents the user from receiving private messages.                                                  | [deaf](/3/modules/deaf)
u_censor        | G         | Switch | *None*          | Anyone                                 | Enables censoring messages sent to the user.                                                        | [censor](/3/modules/censor)
hideoper        | H         | Switch | *None*          | Server operators                       | Hides the user's server operator status from unprivileged users.                                    | [hideoper](/3/modules/hideoper)
hidechans       | I         | Switch | *None*          | Anyone                                 | Hides the channels the user is in from their `/WHOIS` response.                                     | [hidechans](/3/modules/hidechans)
antiredirect    | L         | Switch | *None*          | Anyone                                 | Prevents users from being redirected by channel mode `L` (redirect).                                | [redirect](/3/modules/redirect)
override        | O         | Switch | *None*          | Server operators                       | Allows server operators to opt-in to overriding restrictions.                                       | [override](/3/modules/override)
regdeaf         | R         | Switch | *None*          | Anyone                                 | Prevents users who are not logged into a services account from messaging the user.                  | [services_account](/3/modules/services_account)
u_stripcolor    | S         | Switch | *None*          | Anyone                                 | Enables stripping of IRC formatting codes from private messages.                                    | [stripcolor](/3/modules/stripcolor)
u_noctcp        | T         | Switch | *None*          | Anyone                                 | Enables blocking private messages that contain CTCPs.                                               | [noctcp](/3/modules/noctcp)
showwhois       | W         | Switch | *None*          | Depends on &lt;showwhois:opersonly&gt; | Informs the user when someone does a `/WHOIS` query on their nick.                                  | [showwhois](/3/modules/showwhois)
<!-- end module user modes -->
