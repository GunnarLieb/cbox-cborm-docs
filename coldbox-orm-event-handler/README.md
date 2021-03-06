# ColdBox ORM Event Handler

By using the ColdBox ORM event handler as your base class for your application's event handler you will inherently get the ability to talk to your ColdBox application instance and even inject objects into your ColdFusion ORM entities using [WireBox](http://wiki.coldbox.org/wiki/WireBox.cfm). Not only that but we have also enabled the event handler to re-transmit the Hibernate Interceptions and announce them as ColdBox Interceptions. This way, you can intercept very easily the ColdBox way, create several chains, etc. The first thing you need to do is tell the CF Engine that you want to enable event handling and also which CFC will handle your global ORM entity events.

Important: You can also use the [WireBox-EntityInjection](http://wiki.coldbox.org/wiki/WireBox-EntityInjection.cfm) approach which allows your event handler to be portable between ColdBox and Non-ColdBox applications and also allows you to NOT even create an event handler but just point it to the appropriate class.

