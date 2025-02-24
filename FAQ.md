NetGuard
========

Please scroll down if you want to ask a question, request a feature, or report a bug.

Frequently Asked Questions (FAQ)
--------------------------------

<a name="faq0"></a>
**(0) How do I use NetGuard?**

* Enable the NetGuard firewall using the switch in NetGuard's action bar
* Allow (greenish\*) or deny (reddish\*) Wi-Fi or mobile internet access using the icons next to an application name in NetGuard's applications list

You can use *Settings > Defaults* to change from block/blacklist mode (disable *Block Wi-Fi* and *Block mobile*, and then block unwanted applications in NetGuard's applications list) to allow/whitelist mode (enable *Block Wi-Fi* and *Block mobile*, and then allow desired applications in NetGuard's applications list).

\* Depending on the theme you use, the icons may be:
* Allowed (internet access permitted): greenish (teal) / blue / purple / gray
* Blocked (internet access denied): reddish (salmon) / orange / yellow / amber

<a name="faq1"></a>
**(1) Can NetGuard completely protect my privacy?**

No - nothing can completely protect your privacy.
NetGuard will do its best, but it is limited by the fact it must use the Android VPN service.
This is the trade-off required to make a firewall which does not require root access.
The firewall can only start when Android "allows" it to start,
so it will not offer protection during early boot-up (although you can disable your network before rebooting).
Also, the Android VPN service needs to be restarted to apply new rules when connectivity has changed or when the screen is being turned on or off.
It will, however, be much better than nothing.

In the advanced options you can enable *Seamless VPN handover on reload* to prevent traffic from leaking when the Android VPN service is being restarted.
However, this does not work properly on all Android versions/variants causing NetGuard to hang and block all connections.

On Android N and later NetGuard can be configured as [Always-On VPN](https://developer.android.com/guide/topics/connectivity/vpn#always-on).
On Android O **do not** enable the sub option '*Block connections without VPN*', see [question 51](#user-content-faq51)) for more information on this.

To protect yourself more, remember to disable Wi-Fi and mobile data before rebooting,
and only enable them on reboot, after the firewall service has started (and the key icon is visible in the status bar).

Thanks @[pulser](https://github.com/pulser/)

<a name="faq2"></a>
**(2)  Can I use another VPN application while using NetGuard**

If the VPN application is using the [VPN service](http://developer.android.com/reference/android/net/VpnService.html),
then no, because NetGuard needs to use this service. Android allows only one application at a time to use this service.

NetGuard is a firewall application, so there is no intention to add VPN support.
However, NetGuard supports a [SOCKS5 proxy](https://en.wikipedia.org/wiki/SOCKS) to chain VPN applications.

<a name="faq3"></a>
**(3) Can I use NetGuard on any Android version?**

No, the minimum required Android version is 5.1 (<a href= "https://developer.android.com/about/versions/lollipop">Lollipop</a>)

<a name="faq4"></a>
**(4) Will NetGuard use extra battery power?**

By default NetGuard will hardly use any battery power.
All settings resulting in extra battery usage, like IP filtering and logging, have a warning.
If NetGuard uses a lot of battery power, please double check your settings.

The battery usage when IP filtering is enabled depends on the quality of your Android VPN service implementation and the efficiency of the processor of your device.
Generally the battery usage on older devices might be unacceptable, yet hardly noticeable on modern devices with an efficient processor.

The network speed graph notification will use extra battery power.
This is why the notification is shown only when the screen is on.
You can decrease the update frequency using the settings to reduce the battery usage.

Note that Android often incorrectly contribute battery usage of other apps to NetGuard,
because the network traffic of other apps is flowing through NetGuard.
This means that it might look like NetGuard is using a lot of battery power,
but that in fact the total battery usage of all apps is still the same.

<a name="faq6"></a>
**(6) Will NetGuard send my internet traffic to an external (VPN) server?**

No, depending on the mode of operation basically one of two things will happen with your internet traffic:

* When IP filtering is disabled, blocked internet traffic will be routed into the local VPN service, which will operate as a sinkhole (in effect dropping all blocked traffic)
* When IP filtering is enabled, both blocked and allowed internet traffic will be routed into the local VPN service and only allowed traffic will be forwarded to the intended destination (and not to a VPN server)

The [Android VPN service](http://developer.android.com/reference/android/net/VpnService.html) is being used to locally route all internet traffic to NetGuard so no root is required to build this firewall application.
NetGuard, unlike all other no-root firewalls applications, is 100% open source, so when you are in doubt you can check [the source code](https://github.com/M66B/NetGuard/) yourself.

<a name="faq7"></a>
**(7) Why are applications without internet permission shown?**

Internet permission can be granted with each application update without user consent.
By showing all applications, NetGuard allows you to control internet access even *before* such an update occurs.

<a name="faq8"></a>
**(8) What do I need to enable for the Google Play™ store app to work?**

You need 3 packages (applications) enabled (use search in NetGuard to find them quickly):

* com.android.vending (Play store)
* com.google.android.gms (Play services)
* com.android.providers.downloads (Download manager)

Since the Google Play™ store app has a tendency to check for updates or even download them all by itself (even if no account is associated),
one can keep it in check by enabling "*Allow when screen is on*" for all 3 of these packages.
Click on the down arrow on the left side of an application name and check that option,
but leave the network icons set to red (hence blocked).  The little human icon will appear for those packages.

Note that NetGuard does *not* require any Google service to be installed.

<a name="faq9"></a>
**(9) Why is the VPN service being restarted?**

The VPN service will be restarted when you turn the screen on or off and when connectivity changes (Wi-Fi, mobile)
to apply the rules with the conditions *'Allow when screen is on'* and *'Block when roaming'*.

See [here](http://forum.xda-developers.com/showpost.php?p=65723629&postcount=1788) for more details.

<a name="faq10"></a>
**(10) Will you provide a Tasker plug-in?**

No, because if Tasker is allowed to disable NetGuard, any application can disable NetGuard.
Allowing a security application to be disabled by other applications is not a good idea.

<a name="faq13"></a>
**(13) How can I remove the ongoing NetGuard entry in the notification screen?**

* Long click the NetGuard notification
* Tap the 'i' icon
* Depending on your device and/or ROM manufacturer's software customizations, you can be directed to either:
  * the **App Info** screen and you can uncheck '*Show notifications*' and agree to the next dialog
  * the **App Notifications** screen and you can toggle the '*Block*' slider to on

Note that, whether or not you get a dialog warning to agree upon,
this operation will also disable any information or warning notifications from NetGuard,
such as the new application installed notification.

To read about the need for the notification in the first place, see [question 24](#user-content-faq24).

Some Android versions display an additional notification, which might include a key icon.
This notification, unfortunately, cannot be removed.

<a name="faq14"></a>
**(14) Why can't I select OK to approve the VPN connection request?**

There might be another (invisible) application on top of the VPN connection request dialog.
Some known (screen dimming) applications which can cause this are *Lux Brightness*, *Night Mode*, and *Twilight*.
To avoid this problem, at least temporarily, close all applications and/or services which may be running in the background.

<a name="faq15"></a>
**(15) Are F-Droid builds supported?**

F-Droid builds are not supported because I have no control over if and when the F-Droid version of NetGuard will be updated,
so I cannot guarantee timely updates, for example if there is a critical or security issue.

Because F-Droid builds and GitHub releases are signed differently, an F-Droid build needs to be uninstalled first to be able to update to a GitHub release.

<a name="faq16"></a>
**(16) Why are some applications shown dimmed?**

Disabled applications and applications without internet permission are shown dimmed.

<a name="faq17"></a>
**(17) Why is NetGuard using so much memory?**

It isn't.  NetGuard doesn't allocate any memory, except a little for displaying the user interface elements and for buffering traffic.
It appears, on some Android variants, that the Google Play™ store app connection uses almost 150 MB.  It is needed for in-app donations,
and is incorrectly attributed to NetGuard instead to the Google Play™ store app.

<a name="faq18"></a>
**(18) Why can't I find NetGuard in the Google Play™ store app?**

NetGuard requires at least Android 5.1, so it is not available in the Google Play™ store app on devices running prior Android versions.

<a name="faq19"></a>
**(19) Why does application XYZ still have internet access?**

If you block internet access for an application, there is no way around it.
However, applications could access the internet through other (system) applications/components.
For example, Google Play services receives incoming push messages and ads for most applications, including WhatsApp and Facebook messenger.
You can prevent this by blocking internet access for the other application/component as well.
You can block system applications and components, like Google Play services, by enabling the advanced NetGuard option *Manage system apps*.
This can best be diagnosed by checking the global access log (three dot menu, *Show log*).

Note that some applications keep trying to access the internet, which is done by sending a connection request packet.
This packet goes into the VPN sinkhole when internet access for the application is blocked.
This packet consists of less than 100 bytes and is counted by Android as outgoing traffic
and will be visible in the speed graph notification as well.

<a name="faq20"></a>
**(20) Can I Greenify/hibernate NetGuard?**

No. [Greenifying](https://play.google.com/store/apps/details?id=com.oasisfeng.greenify)
or otherwise hibernating NetGuard will result in rules not being applied
when connectivity changes from Wi-Fi/mobile, screen on/off, and roaming/not roaming.

<a name="faq21"></a>
**(21) Does doze mode affect NetGuard?**

I am not sure, because the [doze mode documentation](http://developer.android.com/training/monitoring-device-state/doze-standby.html)
is not clear if the [Android VPN service](http://developer.android.com/reference/android/net/VpnService.html) will be affected.

To be sure, you can disable battery optimizations for NetGuard manually like this:

```
Android settings > Battery > three dot menu > Battery optimizations > Dropdown > All apps > NetGuard > Don't optimize > Done
```

The procedure to accomplish this can vary between devices.

Disabling doze mode for NetGuard cannot be done from within NetGuard
because, according to Google, NetGuard is [not an application type allowed to do this](http://developer.android.com/training/monitoring-device-state/doze-standby.html#whitelisting-cases).

<a name="faq22"></a>
**(22) Can I tether (use the Android hotspot) / use Wi-Fi calling while using NetGuard?**

Yes, but you'll need to enable subnet routing and tethering in the NetGuard network settings.
Whether or not it works depends on your Android version
because some Android versions have a bug preventing tethering and the VPN service working together.

Some devices hibernate Wi-Fi, preventing tethering from working when the screen is off.
This behavior can be disabled in the Android enhanced/advanced Wi-Fi settings.

<a name="faq24"></a>
**(24) Can you remove the notification from the status bar?**

Android can kill background services at any time.
This can only be prevented by turning a background service into a foreground service.
Android requires an ongoing notification for all foreground services
to make you aware of potential battery usage (see [question 4](#user-content-faq4)).
So, the notification cannot be removed without causing instability.
However, the notification is being marked as low priority,
which should result in moving it to the bottom of the list.

The key icon and/or the VPN running notification,
which is shown by Android and not by NetGuard, unfortunately, cannot be removed.
The [Google documentation](http://developer.android.com/reference/android/net/VpnService.html) states:
*"A system-managed notification is shown during the lifetime of a VPN connection"*.

Android 8 Oreo and later display a notification "*... running in the background*" listing all apps running in the background.
You can't disable this notification, but you can remove the icon from the status bar like this:

* Open Settings > Apps & notifications > App info
* Open settings (three dots); Select "Show system"
* Select "Android System"
* Select "App notifications"
* Select "Apps running in background"
* Select "Importance" and select "Low"

<a name="faq25"></a>
**(25) Can you add a 'Select All' function?**

There is no need for a 'Select All' function
because you can switch from block (blacklist) to allow (whitelist) mode using Netguard's settings.
See also [question 0](#user-content-faq0).

<a name="faq27"></a>
**(27) How do I read the blocked traffic log?**

The columns have the following meanings:

1. Time (tap on a log entry to see the date)
1. Application icon (tap on a log entry to see the application name)
1. Application UID
1. Wi-Fi / mobile connection, green=allowed, red=blocked
1. Interactive state (screen on or off)
1. Protocol (see below) and packet flags (see below)
1. Source and destination port (tap on a log entry to lookup a destination port)
1. Source and destination IPv4 or IPv6 address (tap on a log entry to lookup a destination IP address)
1. Organization name owning the IP address (needs to be enabled via the menu)

Protocols:

* HOPO ([IPv6 Hop-by-Hop Option](https://en.m.wikipedia.org/wiki/IPv6_packet#Hop-by-hop_options_and_destination_options))
* ICMP
* IGMP
* ESP (IPSec)
* TCP
* UDP
* Number = one of the protocols in [this list](https://en.wikipedia.org/wiki/List_of_IP_protocol_numbers)
* 4 = IPv4
* 6 = IPv6

Packet flags:

* S = SYN
* A = ACK
* P = PSH
* F = FIN
* R = RST

For a detailed explanation see [here](https://en.wikipedia.org/wiki/Transmission_Control_Protocol).

Only TCP, UDP, and ICMP ping traffic can be routed through the Android VPN service.
All other traffic will be dropped and will be shown as blocked in the global traffic log.
This is almost never a problem on an Android device.

<a name="faq28"></a>
**(28) Why is Google connectivity services allowed internet access by default?**

The Google connectivity services system application checks if the current network is really connected to the internet.
This is probably accomplished by briefly connecting to some Google server.

If this is not the case, there will be an '!' in the Wi-Fi or mobile icon in the system status bar.

Recent Android versions seem not to switch connectivity from mobile to Wi-Fi when the Wi-Fi network is not really connected,
even though there is a connection to the Wi-Fi network (or the other way around). On Android 6.0 and later you might get a notification asking you if you want to keep this connection on or not.
To prevent a bad user experience, NetGuard includes a predefined rule to default allow the Google connectivity services.

You can find all predefined rules [here](https://github.com/M66B/NetGuard/blob/master/app/src/main/res/xml/predefined.xml).

You can override predefined rules.

<a name="faq29"></a>
**(29) Why do I get 'The item you requested is not available for purchase'?**

You can only purchase pro features when you have installed NetGuard from the Google Play store.

<a name="faq30"></a>
**(30) Can I also run AFWall+ on the same device?**

Unless you are just testing NetGuard, there is no current reason to use them both, since they cover the same function (firewall),
although with different base needs (AFWall+ needs a rooted device) and ways of doing their thing (AFWall+ uses iptables whereas NetGuard uses a VPN).

Also you need to keep per application access rules _always_ in sync between AFWall+ and NetGuard,
else the application will not be able to access the network,
hence bringing another level of complexity when setting and assuring everything work as expected.

Some pointers on how to set up AFWall+ to be used simultaneously with NetGuard:
* if not using filtering in NetGuard, applications _need_ direct internet access (Wi-Fi and/or mobile) in AFWall+
* if using filtering, NetGuard will _need_ internet access (Wi-Fi and/or mobile) in AFWall+
* if using filtering, when you un/reinstall NetGuard, remember to re-allow NetGuard in AFWall+
* if using filtering, applications _need_ VPN internet access (check the box to show that option in AFWall+ settings)

This question was community contributed. There is no support on using NetGuard and AFWall+ together.

<a name="faq31"></a>
**(31) Why can some applications be configured as a group only?**

For many purposes, including network access, Android groups applications on UID and not on package/application name.
Especially system applications often have the same UID, despite having a different package and application name; these are set up like this by the ROM manufacturer at build time.
These applications can only be allowed/blocked access to the internet as a group.

<a name="faq32"></a>
**(32) Why is the battery/network usage of NetGuard so high?**

This is because Android counts battery and network usage which is normally counted for other applications
against NetGuard in IP filtering mode. The total battery usage is slightly higher when IP filtering mode is enabled.
IP filtering mode is always enabled on Android versions prior to 5.0, and optionally enabled on later Android versions.

<a name="faq33"></a>
**(33) Can you add profiles?**

Profiles are inconvenient because they need to be operated manually.
Conditions like '*When screen is on*' are, on the other hand, convenient because they work automatically.
Therefore profiles will not be added, but you are welcome to propose new conditions;
however, they need to be generally usable to be included.

As a workaround you can use the export/import function to apply specific settings in specific circumstances.
Alternatively, you can use lockdown mode as a profile.

<a name="faq34"></a>
**(34) Can you add a condition 'when on foreground' or 'when active'?**

Recent Android versions do not allow an application to query if other applications are in the foreground/background or active/inactive
without holding an [additional privacy violating permission](https://developer.android.com/reference/android/Manifest.permission.html#PACKAGE_USAGE_STATS)
and at the expense of extra battery usage (because periodic polling is required).
As a result, this cannot be added without significant disadvantages, like [this one](http://www.xda-developers.com/working-as-intended-an-exploration-into-androids-accessibility-lag/).
You can use the condition '*when screen is on*' instead.

<a name="faq35"></a>
**(35) Why does the VPN not start?**

NetGuard "asks" Android to start the local VPN service,
but some Android versions contain a bug which prevents the VPN from starting (automatically).
Sometimes this is caused by updating NetGuard.
Unfortunately this cannot be fixed by NetGuard.
You can try to restart your device and/or revoke the VPN permissions from NetGuard using the Android settings.
Sometimes it helps to uninstall and install NetGuard again (be sure to export your settings first!).

<a name="faq36"></a>
**(36) Can you add PIN or password protection?**

Since turning off the VPN service using the Android settings cannot be prevented,
there is little use in adding PIN or password protection.

<a name="faq37"></a>
**(37) Why are the pro features so expensive?**

The right question is "*why are there so many taxes and fees*":

* VAT: 25% (depending on your country)
* Google fee: 30%
* Income tax: 50%

So, what is left for the developer is just a fraction of what you pay.

Despite NetGuard being *really* a lot of work, only some of the convenience and advanced features need to be purchased,
which means that NetGuard is basically free to use
and that you don't need to pay anything to reduce your data usage, increase battery life, and increase your privacy.

Also note that most free applications will appear not to be sustainable in the end, whereas NetGuard is properly maintained and supported,
and that free applications may have a catch, like sending privacy sensitive information to the internet.

See [here](http://forum.xda-developers.com/showpost.php?p=67892427&postcount=3030) for some more information.

<a name="faq38"></a>
**(38) Why did NetGuard stop running?**

First of all, please make sure you disabled battery optimizations for NetGuard in the Android settings.

On most devices, NetGuard will keep running in the background with its foreground service.
On some devices (in particular some Samsung models), where there are lots of applications competing for memory, Android may still stop NetGuard as a last resort.
Some Android versions, in particular of Huawei (see [here](https://www.forbes.com/sites/bensin/2016/07/04/push-notifications-not-coming-through-to-your-huawei-phone-heres-how-to-fix-it/) for a fix) or Xiaomi (see [here](https://www.forbes.com/sites/bensin/2016/11/17/how-to-fix-push-notifications-on-xiaomis-miui-8-for-real/) for a fix) stop apps and services too aggressively.
Unfortunately this cannot be fixed by NetGuard, and can be considered a shortcoming of the device and/or as a bug in Android.
As a matter of fact lots of apps suffer from this, see the website [Don't kill my app!](https://dontkillmyapp.com/) for more information and solutions.
You can workaround this problem by enabling the watchdog in the NetGuard advanced options to check every 10-15 minutes.

<a name="faq39"></a>
**(39) How does a VPN based firewall differ from a iptables based firewall?**

See this [Stack Exchange question](http://android.stackexchange.com/questions/152087/any-security-difference-between-root-based-firewall-afwall-and-non-root-based).

<a name="faq40"></a>
**(40) Can you add schedules?**

Besides not being trivial to add, schedules - in my opinion - are not a good idea, since time is not a good rule condition.
A rule condition like *When screen is on* is a better and more straightforward condition.
Therefore schedules will not be added, but you are welcome to propose other new conditions.

<a name="faq41"></a>
**(41) Can you add wildcards / address/port ranges?**

Wildcards to allow/block addresses and address/port ranges would have a significant performance and usability impact and therefore will not be added.
Wildcards rules and address/port ranges would need to be checked for each and every connection attempt.
Since NetGuard blocks, unlike any other no-root firewall, domain names instead of IP addresses there is hardly a need for wildcards.

<a name="faq42"></a>
**(42) Why is permission ... needed?**

* INTERNET ('*Full network access*'): to forward allowed (filtered) traffic to the internet
* ACCESS_NETWORK_STATE ('*View network connections*'): to check if the device is connected to the internet through Wi-Fi
* READ_PHONE_STATE ('*Device ID & call information*'): to detect mobile network changes, see [here](http://forum.xda-developers.com/showpost.php?p=64107371&postcount=489) for more details
* ACCESS_WIFI_STATE ('*Wi-Fi connection information*'): to detect Wi-Fi network changes
* RECEIVE_BOOT_COMPLETED ('*Run at startup*'): to start the firewall when booting the device
* WAKE_LOCK ('*Prevent device from sleeping*'): to reliably reload rules in the background on connectivity changes
* VIBRATE: to provide vibration feedback on widget tap
* FOREGROUND_SERVICE ('foreground service'): to run a foreground service on Android 9 Pie and later
* QUERY_ALL_PACKAGES: to list all apps on Android 11 and later
* BILLING: to use in-app billing

<a name="faq43"></a>
**(43) I get 'This app is causing your device to run slowly'**

This message is displayed by the *Smart Manager*,
but actually it is the 'Smart' Manager application itself which is causing delays and lags.
Some links:

* [Smart Manager complaining about LastPass](https://www.reddit.com/r/GalaxyS6/comments/3htu2y/smart_manager_cmoplaining_about_lastpass/)
* [Disable Smart Manager?](http://forums.androidcentral.com/samsung-galaxy-s4/595483-disable-smart-manager.html)

<a name="faq44"></a>
**(44) I don't get notifications on access**

To prevent a high number of status bar notifications, notify on access is done only once per domain name per application.
Access to domain names shown in the application access log (drill down in the NetGuard application settings) will not be notified again,
even if you just enabled notify on access.
To get notified for all domain names again, you can clear the application access log using the trashcan icon.
If you want to clear all applications logs, you can export and import your settings.

Another reason why you don't get notifications could be an applied "Power Saving Mode" for example on Samsung devices. Even if you do not restrict CPU frequency in this mode.

<a name="faq45"></a>
**(45) Does NetGuard handle incoming connections?**

The Android VPN service handles outgoing connections only (from applications to the internet), so incoming connections are normally left alone.

If you want to run a server application on Android, then be aware that using port numbers below 1024 require root permissions
and that some Android versions contain routing bugs, causing inbound traffic incorrectly being routed into the VPN.

<a name="faq46"></a>
**(46) Can I get a refund?**

If a purchased pro feature doesn't work [as described](https://www.netguard.me/)
and this isn't caused by a problem in the free features
and I cannot fix the problem in a timely manner, you can get a refund.
In all other cases there is no refund possible.
In no circumstances there can be a refund for any problem related to the free features,
since there wasn't paid anything for them and because they can be evaluated without any limitation.
I take my responsibility as seller to deliver what has been promised
and I expect that you take responsibility for informing yourself of what you are buying.

<a name="faq48"></a>
**(48) Why are some domain names blocked while they are set to be allowed?**

NetGuard blocks traffic based on the IP addresses an application is trying to connect to.
If more than one domain name is on the same IP, they cannot be distinguished.
If you set different rules for 2 domains which resolve to the same IP, both will be blocked.

Thanks @[pulser](https://github.com/pulser/)

Another potential problem is that Android doesn't honor the DNS TTL value and applies its own caching rules.
This could result in NetGuard too early or too late purging a DNS record from its own cache,
resulting in not recognizing an IP address or recognizing a wrong IP address.
You can try to workaround this by changing the DNS TTL value setting of NetGuard.
This value is used as a minimum DNS TTL value in an attempt to mimick the behavior of Android.

NetGuard will also block traffic while restarting the Android VPN service to apply new rules,
for example when connectivity changes or when the screen is turned on or off.

<a name="faq49"></a>
**(49) Does NetGuard encrypt my internet traffic / hide my IP address?**

NetGuard is a firewall application that filters internet traffic on your device (see also [this question](#user-content-faq6)),
so it is not meant to - and does not - encrypt your internet traffic or hide your IP address.

<a name="faq50"></a>
**(50) Will NetGuard automatically start on boot?**

Yes, NetGuard will automatically be started on boot if you powered off your device with NetGuard enabled and NetGuard is not installed on external storage.

Some devices, for example OnePlus and Mi devices, can prevent certain apps from auto-starting after reboot.
This can be disabled in the Android settings.

<a name="faq51"></a>
**(51) Why does NetGuard block all internet traffic?!**

Make sure you have put NetGuard on the doze exception list (Android 6 Marshmallow or later)
and that Android allows NetGuard to use the internet in the background (see also [this question](#user-content-faq21)).

Make sure you are not running NetGuard in allow (whitelist) mode (check the NetGuard default settings).

Make sure you didn't enable the Always-On VPN sub option '*Block connections without VPN*' (Android 8 Oreo or later).
This will block resolving domain names too (is it a bug or feature?).

Some Android versions, including LineageOS and /e/ for some devices, contain a bug resulting in all internet traffic being blocked.
Mostly, you can workaround this bug by enabling filtering in NetGuard's *Advanced options*.
If this doesn't solve the issue, the problem can unfortunately not be fixed or worked around by NetGuard.
Please [see here](https://forum.xda-developers.com/t/app-6-0-netguard-no-root-firewall.3233012/post-84457527) for a fix.

<a name="faq52"></a>
**(52) What is lockdown mode?**

In lockdown mode, all traffic for all applictions will be blocked,
except for applications with the condition *'Allow in lockdown mode'* enabled.
You can use this mode to limit battery usage or network usage,
for example, when your battery is almost empty or when your data allotment is almost exhausted.

Note that Lockdown mode applies only if the corresponding option is also set in "Network options" 
(one for Wi-Fi mode, one for Mobile data), allowing to have lockdown in only one of the two network modes 
and not in the other (eg. Lock down if mobile data are active, but not if Wi-Fi is currently used).

Note also that system applications will only be blocked in this mode
when managing system applications is enabled in the advanced settings.

You can enable/disable lockdown mode in the main menu, using a widget, or using a settings tile (Android 7 Nougat or later).

<a name="faq53"></a>
**(53) The translation in my language is missing / incorrect / incomplete**

You can contribute translations [here](https://crowdin.com/project/netguard) (registration is free).
If your language is missing, please contact me to have it added.

<a name="faq54"></a>
**(54) How to tunnel all TCP connections through the Tor network?**

Tor with NetGuard is only supported in the [XDA NetGuard forum](http://forum.xda-developers.com/showthread.php?t=3233012).
There is no personal support on Tor with NetGuard, because I don't use Tor myself.

First, install [Orbot](market://details?id=org.torproject.android), the Android client for Tor,
run it, press _Start_, while it connects open its _Settings_ and make sure it's setup to auto-start
on device start.

In NetGuard's _Network options_ enable _Subnet routing_ and in _Advanced options_ toggle on
_Use SOCKS5 proxy_ with address 127.0.0.1 and port as 9050 (this is the default port, if you changed
this in Orbot make the adjustment here also).

This should be enough, if testing fails (eg. no connection at all) you can open the app details
for Orbot, uncheck _Apply rules and conditions_ and retry.

How to test: open Firefox (or another non-proxy enabled browser) to the address https://ipleak.net/
and you should see a different IP address from your regular one, and below in the _Tor Exit Node_
field something else besides _Unknown_.

**Be aware** that all the other Tor caveats (https://www.torproject.org/docs/faq.html.en) still apply,
like having the Tor network unreacheable, your activity actively monitored/targeted in your country,
online services (eg. Gmail, Google Play store) failing to login or being forced to solve endless capchas
when accessing sites that use Cloudflare's CDN services.

<a name="faq55"></a>
**(55) Why does NetGuard connect to Amazon / ipinfo.io / 216.239.34.21?**

NetGuard connects to Amazon / [ipinfo.io](https://ipinfo.io/) to show the names and organizations for IP addresses.
If you don't want this, just disable showing names and organizations using the three dot menu in the global log view.

<a name="faq56"></a>
**(56) Why does NetGuard allow all internet traffic?!**

NetGuard can block each and every application, even system applications and components.

NetGuard, by default, allows all traffic to prevent hard to find problems.  You need to selectively block traffic yourself by tapping on the mobile or Wi-Fi icons.

Be aware that NetGuard will allow traffic to an application when the screen is on and the condition *'when screen on'* is enabled.

<a name="faq57"></a>
**(57) Why does NetGuard use so much data?**

Basically, NetGuard doesn't use data itself.
However, many Android versions incorrectly account data of other applications flowing through NetGuard to NetGuard instead of to the applications.
The data usage of other applications will be zero with NetGuard enabled in this case.

The total data usage of your device will be the same with and without NetGuard.

<a name="faq58"></a>
**(58) Why does loading the application list take a long time?**

The application list is provided by Android, so the loading speed depends mostly on the power of your device and on the efficiency of your Android version.
For example shortage of memory could lead to increased loading times, because memory needs to be freed, for example by pausing other applications.

In some circumstances, restricting system apps and system components is known to cause the application list to load slowly or not at all. The exact circumstances are unknown.

<a name="faq59"></a>
**(59) Can you help me restore my purchase?**

Google manages all purchases, so as a developer I have no control over purchases.
So, the only thing I can do, is give some advice:

* Make sure you have an active internet connection
* Make sure you didn't block Google Play store / Play services
* Make sure you are logged in with the right Google account and that there is nothing wrong with your Google account
* Make sure you installed NetGuard via the right Google account if you configured multiple Google accounts on your device
* Open the Play store app and wait at least a minute to give it time to synchronize with the Google servers
* Open NetGuard and navigate to the pro features screen; NetGuard will check the purchases again

You can also try to clear the cache of the Play store app via the Android apps settings.

Note that:

* Purchases are stored in the Google cloud and cannot get lost
* There is no time limit on purchases, so they cannot expire
* Google does not expose details (name, e-mail, etc) about buyers to developers
* An app like NetGuard cannot select which Google account to use
* It may take a while until the Play store app has synchronized a purchase to another device
* Play Store purchases cannot be used without the Play Store, which is also not allowed by Play Store rules

If you cannot solve the problem with the purchase, you will have to contact Google about it.

<a name="faq60"></a>
**(60) Why does IP (Wi-Fi) calling/SMS/MMS not work?**

Please see the [compatibility section](https://github.com/M66B/NetGuard/#compatibility) about this
(you might need to request the desktop version to see this section if you are using a mobile device).

<a name="faq61"></a>
**(61) Help, NetGuard crashed!**

NetGuard rarely crashes ("unexpectedly stopped"), but if it crashed (which is something different than being stopped by Android, see [this FAQ](#user-content-faq38)),
then it is mostly caused by bugs in your Android version
(either in the [Android VPN service](https://developer.android.com/reference/android/net/VpnService.html) implementation or in the [Android Linux kernel](https://developer.android.com/guide/platform/index.html#linux-kernel)).
I am happy to check what the cause of a crash is and I will fix it whenever possible, but I need a logcat captured from your PC with the crash log for this.
Since logcats are mostly quite large, I will need the exact time of the crash as well.
If you don't know how to capture a logcat from your PC, please use your favorite search engine to find one of the numerous guides.

<a name="faq62"></a>
**(62) How can I solve 'There was a problem parsing the package' ?**

Likely causes are that the downloaded APK file is damaged (which could be caused by a virus scanner)
or that you are trying to install NetGuard on a not supported Android version.

<a name="faq63"></a>
**(63) Why is all DNS traffic allowed?**

NetGuard blocks unlike any other Android firewall on real domain names.
For this a list of domain names and IP address needs to be built.
For this purpose, NetGuard allows all DNS traffic, even if the domain name is listed in the hosts file.
However, this doesn't mean traffic to the resolved IP address is allowed.

If you don't trust the system (Google's) or your provider's DNS servers, you can set alternative DNS servers in the advanced settings.
Be sure to enter and confirm the addresses and to set two DNS server addresses.
If you enter just one DNS server address, it will be used in addition to the default DNS server addresses.

<a name="faq64"></a>
**(64) Can you add DNS over TLS?**

If you mean to intercept [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS) requests to resolve domain names,
this is not possible because DNS over TLS traffic is encrypted, which is the whole point of DNS over TLS.

If you mean to translate plain DNS to DNS over TLS, Android 9 Pie and later already support DNS over TLS out of the box,
so it isn't worth the significant effort to add this.

<br />

<a name="faq65"></a>
**(65) Why can NetGuard not block itself?**

First of all, if NetGuard could block itself, you should trust that NetGuard really blocks itself,
which is basically the same as trusting that NetGuard doesn't connect to the internet when not needed.

Note that NetGuard needs to connect to the internet to forward traffic of other apps to the internet and to lookup information on IP addresses,
see also [this FAQ](#user-content-faq55).

NetGuard could block itself in older versions,
but this required calling [VpnService.protect](https://developer.android.com/reference/android/net/VpnService.html#protect(int)) for each and every connection.
Since there are lots of connections of lots of apps in a typical Android environment,
this resulted in wasting battery power and in crashes on some Android versions with bugs in this function.

So, because blocking NetGuard with itself didn't added anything useful
and to save on battery power and to prevent crashes blocking NetGuard with itself was removed.

<br />

<a name="faq66"></a>
**(66) Why is a blocked app still accessing the internet?**

Blocked apps cannot access the internet. There are no exceptions to this.

However:

* Apps can show locally cached content
* Incoming (push) messages are received by the system component Google Play services and not apps, especially when the app is in the background or when the screen is turned off
* Similarly, advertisements are mostly received by the system component Google Play services
* Downloads are often performed by the download manager and not apps

If you like to block Google Play services or the download manager, you'll need to enable managing system apps in the advanced settings.

If you like to make sure that push messages will always be received, you can disable *Apply rules and conditions* for Google Play services.

To be clear: in most cases **you cannot block ads by blocking apps**.
However, you can block ads for all apps with NetGuard, please see [here](https://github.com/M66B/NetGuard/blob/master/ADBLOCKING.md) about how to.

<br />

<a name="faq67"></a>
**(67) Who is 'nobody'?**

["nobody" is the conventional name of a user account](https://en.wikipedia.org/wiki/Nobody_(username))
which owns no files, is in no privileged groups, and has no abilities except those which every other user has.

<br />

**NetGuard is supported for phones and tablets only, so not for other device types like televisions or vehicles.**

**If you didn't find the answer to your question, you can ask your questions [in this forum](http://forum.xda-developers.com/showthread.php?t=3233012) or contact me by using [this contact form](https://contact.faircode.eu/)**.
