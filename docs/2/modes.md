---
title: v2 Modes
---

{! 2/_support.md !}

## InspIRCd Modes

InspIRCd supports five types of mode:

Type      | Parameter when adding?       | Parameter when removing?     | Can be set multiple times?       | Description
--------- | ---------------------------- | ---------------------------- | -------------------------------- | -----------
Switch    | No                           | No                           | No                               | Toggles the behaviour of a feature on a channel or user.
Parameter | Yes                          | No                           | No                               | Enables and configures the behaviour of a feature on a channel or user.
ParamBoth | Yes                          | Yes                          | No                               | The same as a Parameter mode only the parameter must be specified to remove it.
Prefix    | Yes; channel member nickname | Yes; channel member nickname | Yes; once per channel member     | Grants/revokes a status rank to the user specified in the parameter.
List      | Yes                          | Yes                          | Yes; up to the maximum list size | Adds/removes entries from a list.

### Core Channel Modes

Name       | Character | Type      | Parameter Syntax | Description
---------- | --------- | --------- | ---------------- | -----------
ban        | b         | List      | `<mask>`         | Bans users matching &lt;mask&gt; from joining the channel.
inviteonly | i         | Switch    | *None*           | Prevents users from joining the channel without an invite.
key        | k         | ParamBoth | `<key>`          | Prevents users from joining the channel who have not specified the &lt;key&gt; password.
limit      | l         | Parameter | `<count>`        | Allows no more than &lt;count&gt; users to join the channel.
moderated  | m         | Switch    | *None*           | Prevents users without a prefix rank from messaging the channel.
noextmsg   | n         | Switch    | *None*           | Prevents users who are not in the channel from messaging the channel.
op         | o         | Prefix    | `<nick>`         | Grants channel operator status to &lt;nick&gt;.
private    | p         | Switch    | *None*           | Hides the channel in `/WHOIS` from people who are not a member. You probably want the `s` (secret) channel mode rather than this.
secret     | s         | Switch    | *None*           | Hides the channel in `/WHOIS` and `/LIST` from people who are not a member.
topiclock  | t         | Switch    | *None*           | Prevents non-channel operators from changing the channel topic.
voice      | v         | Prefix    | `<nick>`         | Grants channel voice status to &lt;nick&gt;.

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

For more details and examples of the channel modes of a specific module please refer to [the appropriate page for that module](/2/modules).

<!-- begin module channel modes -->
Name          | Character | Type      | Paramter Syntax        | Usable By | Description                                                                            | Provided By
--------------|-----------|-----------|------------------------|-----------|----------------------------------------------------------------------------------------|------------------------------------------------
blockcolor    | c         | Switch    | *None*                 | -         | Enables blocking messages that contain IRC formatting codes                            | [blockcolor](/2/modules/blockcolor)
delaymsg      | d         | Parameter | `<seconds>`            | -         | Prevents newly joined users from speaking until                                        | [delaymsg](/2/modules/delaymsg)
banexception  | e         | List      | `<mask>`               | -         | Exempts users matching                                                                 | [banexception](/2/modules/banexception)
flood         | f         | Parameter | `(*)<lines>:<seconds>` | -         | Kicks users who send more than                                                         | [messageflood](/2/modules/messageflood)
filter        | g         | List      | `<glob>`               | -         | Prevents users from sending messages that match                                        | [chanfilter](/2/modules/chanfilter)
joinflood     | j         | Parameter | `<joins>:<seconds>`    | -         | Prevents more than                                                                     | [joinflood](/2/modules/joinflood)
c_registered  | r         | Switch    | *None*                 | -         | Marks the channel as being registered                                                  | [services_account](/2/modules/services_account)
auditorium    | u         | Switch    | *None*                 | -         | Enables auditorium mode                                                                | [auditorium](/2/modules/auditorium)
autoop        | w         | List      | `<status>:<mask>`      | -         | Grants the                                                                             | [autoop](/2/modules/autoop)
operprefix    | y         | Prefix    | `<nick>`               | -         | Grants channel operprefix status to                                                    | [operprefix](/2/modules/operprefix)
sslonly       | z         | Switch    | *None*                 | -         | Prevents users who are not connected using TLS                                         | [sslmodes](/2/modules/sslmodes)
allowinvite   | A         | Switch    | *None*                 | -         | Allows unprivileged users to use the                                                   | [allowinvite](/2/modules/allowinvite)
blockcaps     | B         | Switch    | *None*                 | -         | Enables blocking excessively capitalised messages                                      | [blockcaps](/2/modules/blockcaps)
noctcp        | C         | Switch    | *None*                 | -         | Enables blocking messages that contain CTCPs                                           | [noctcp](/2/modules/noctcp)
delayjoin     | D         | Switch    | *None*                 | -         | Prevents users from receiving JOIN messages until the joining user speaks              | [delayjoin](/2/modules/delayjoin)
nickflood     | F         | Parameter | `<changes>:<seconds>`  | -         | Prevents more than                                                                     | [nickflood](/2/modules/nickflood)
censor        | G         | Switch    | *None*                 | -         | Enables censoring messages sent to the channel                                         | [censor](/2/modules/censor)
history       | H         | Parameter | `<count>:<period>`     | -         | Sends up to                                                                            | [chanhistory](/2/modules/chanhistory)
invex         | I         | List      | `<mask>`               | -         | Exempts users matching                                                                 | [inviteexception](/2/modules/inviteexception)
kicknorejoin  | J         | Parameter | `<seconds>`            | -         | Prevents who have been kicked from rejoining until                                     | [kicknorejoin](/2/modules/kicknorejoin)
noknock       | K         | Switch    | *None*                 | -         | Disables the usage of the                                                              | [knock](/2/modules/knock)
redirect      | L         | Parameter | `<channel>`            | -         | Redirects all new users to                                                             | [redirect](/2/modules/redirect)
regmoderated  | M         | Switch    | *None*                 | -         | Prevents users who are not logged into a services account from speaking in the channel | [services_account](/2/modules/services_account)
nonick        | N         | Switch    | *None*                 | -         | Prevents users from changing their nickname whilst in the channel                      | [nonicks](/2/modules/nonicks)
operonly      | O         | Switch    | *None*                 | -         | Prevents non                                                                           | [operchans](/2/modules/operchans)
permanent     | P         | Switch    | *None*                 | -         | Prevents the channel from being deleted when the last user leaves                      | [permchannels](/2/modules/permchannels)
nokick        | Q         | Switch    | *None*                 | -         | Prevents privileged users from using the                                               | [nokicks](/2/modules/nokicks)
reginvite     | R         | Switch    | *None*                 | -         | Prevents users who are not logged into a services account from joining the channel     | [services_account](/2/modules/services_account)
stripcolor    | S         | Switch    | *None*                 | -         | Enables stripping of IRC formatting codes from channel messages                        | [stripcolor](/2/modules/stripcolor)
nonotice      | T         | Switch    | *None*                 | -         | Enables blocking messages sent with the                                                | [nonotice](/2/modules/nonotice)
exemptchanops | X         | List      | `<restriction>:<mode>` | -         | Exempts users with the                                                                 | [exemptchanops](/2/modules/exemptchanops)
join          | Y         | Prefix    | `<nick>`               | -         | Grants channel official                                                                | [ojoin](/2/modules/ojoin)
namebase      | Z         | List      | `<name>[=<value>]`     | -         | Allows users to add                                                                    | [namedmodes](/2/modules/namedmodes)
<!-- end module channel modes -->

### Core User Modes

Name      | Character | Type      | Parameter Syntax  | Description
--------- | --------- | --------- | ----------------- | -----------
invisible | i         | Switch    | *None*            | Marks the user as invisible.
oper      | o         | Switch    | *None*            | Marks the user as a server operator (can only be set by the server).
snomask   | s         | Parameter | `(+|-)<snomasks>` | Enables receiving the specified types of [server operator notice](/2/snomasks).
wallops   | w         | Switch    | *None*            | Enables receiving `/WALLOPS` messages from server operators.

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

For more details and examples of the user modes of a specific module please refer to [the appropriate page for that module](/2/modules).

<!-- begin module user modes -->
Name            | Character | Type   | Paramter Syntax | Usable By | Description                                                                       | Provided By
----------------|-----------|--------|-----------------|-----------|-----------------------------------------------------------------------------------|------------------------------------------------
deaf_commonchan | c         | Switch | *None*          | -         | Requires other users to have a common channel before they can message this user   | [commonchans](/2/modules/commonchans)
deaf            | d         | Switch | *None*          | -         | Prevents the user from receiving channel messages                                 | [deaf](/2/modules/deaf)
callerid        | g         | Switch | *None*          | -         | Enables whitelisting of who can message the user                                  | [callerid](/2/modules/callerid)
helpop          | h         | Switch | *None*          | -         | Marks the user as being available for help                                        | [helpop](/2/modules/helpop)
servprotect     | k         | Switch | *None*          | -         | Protects services pseudoclients against kicks                                     | [servprotect](/2/modules/servprotect)
u_registered    | r         | Switch | *None*          | -         | Marks the user as being logged into a services account                            | [services_account](/2/modules/services_account)
cloak           | x         | Switch | *None*          | -         | Enables hiding of the user                                                        | [cloaking](/2/modules/cloaking)
bot             | B         | Switch | *None*          | -         | Marks the user as a bot                                                           | [botmode](/2/modules/botmode)
u_censor        | G         | Switch | *None*          | -         | Enables censoring messages sent to the user                                       | [censor](/2/modules/censor)
hideoper        | H         | Switch | *None*          | -         | Hides the user                                                                    | [hideoper](/2/modules/hideoper)
hidechans       | I         | Switch | *None*          | -         | Hides the channels the user is in from their                                      | [hidechans](/2/modules/hidechans)
antiredirect    | L         | Switch | *None*          | -         | Prevents users from being redirected by channel mode                              | [redirect](/2/modules/redirect)
regdeaf         | R         | Switch | *None*          | -         | Prevents users who are not logged into a services account from messaging the user | [services_account](/2/modules/services_account)
u_stripcolor    | S         | Switch | *None*          | -         | Enables stripping of IRC formatting codes from private messages                   | [stripcolor](/2/modules/stripcolor)
showwhois       | W         | Switch | *None*          | -         | Informs the user when someone does a                                              | [showwhois](/2/modules/showwhois)
<!-- end module user modes -->
