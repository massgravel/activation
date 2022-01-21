# Windows 10 Activation

Welcome to the `activation` repo. This will have some info on Windows 10
activation methods and related stuff. Start below.

Preliminary info:
 * **TBV** means "To Be Verified" and is a placeholder for when I don't have time to
   verify something at the time of writing. 
 * In some places the words "licensing" and "activation" might be used
   interchangeably. This is incorrect but try your best to ignore it if you
   really care or actually know the difference.

# Scope

Most of the things I will be writing about here are about Windows 10 activators.
All of the work I've been involved with had to do with Windows 10 activators.
Nothing about Office, 8, 8.1, 7, Vista, XP or anything else so don't expect me
to write anything correctly about those things.

This is not a guide for purchasing Windows either. Licensing is described mainly
in terms of product keys (more on them in due time) associated with its types
and not meant as an article on "the nuances of volume licensing". That would be
boring.

# Windows 10 Activation and Activators

Windows has seen a lot of activators in its time. Instead of fixing the problem
once and for all Microsoft went for uninventing the wheel with Windows 10 and
made fraudulent activation as easy as possible. (As to why they did it, the
reason is likely very simple - they want you to keep using Windows. That's it.)

Windows 10 was, for a time, offered to everyone as a free upgrade from Windows
7, 8 and 8.1. This meant everyone who had an activated copy of those could (and
still technically can) get it free of charge forever.

But first, it might be useful to get a vague understanding of what Windows
licensing even looks like in the first place.

## Windows Licensing

Windows has different types of licensing for different types of customers.
The most familiar names might be:

 * **Retail**
 * **OEM**
 * **Volume**

### Retail Licensing
Microsoft's Retail customers are treated as royalty, they chose to pay Microsoft
for their product directly after all.

The retail license entitles a single user to use Windows on whatever machine
they like for as long as they like. If the user so desires, they can move their
activation onto a different machine but the limit of simultaneously activated
machines is always (in theory) just one.

### OEM Licensing
**Original Equipment Manufacturers**, through an agreement with Microsoft are able
to sell Windows with their hardware. Customers who buy computers with Windows
preinstalled will be licensed to use it **only** on the hardware they bought it
with and are **not** entitled to official Microsoft support.

There are multiple types of keys that will accompany OEM licenses. Those are:

 * **OEM:SLP** (System Locked Pre-installation) 
 * **OEM:NSLP** (Non-System Locked Pre-installation) 
 * **OEM:DM** (Digital Marker) 

The differences between them are pretty extreme but ultimately do not matter
that much. In short, **SLP** keys do not require Microsoft's activation servers
to activate - the OEM marks a machine as activated during manufacturing,
**DM** are the "BIOS keys" you might have seen/heard about and **NSLP**s are for
when the OEM doesn't want to bother with activation during manufacturing. In
terms more people might understand, NSLP is analogous to COA.

### Volume Licensing
Microsoft's bigger customers that "need" more licenses for more computers can opt
in for an easier way to manage and pay their Microsoft overlords for their OS
needs.
Volume licensing offers two ways to activate Microsoft products: via the
internet (or by phone if you're weird) and using KMS servers.

There are three types of keys that will matter for volume licensing. Those are:

 * **Volume:GVLK** (Generic Volume Licensing Key)
 * **Volume:MAK** (Multiple Activation Key)
 * **Volume:CSVLK** (Customer-Specific Volume Licensing Key)

Generic keys are installed on all machines that are to be activated by a KMS
server. Those keys are not specific to customers and are not special in any way;
in fact, every volume licensing cusomer on the planet uses [the same GVLK
keys](https://docs.microsoft.com/en-us/windows-server/get-started/kms-client-activation-keys).
Because Generic keys are generic, they do not activate the system by themselves;
they need a KMS server to do that. The KMS server is "created" by installing a
**CSVLK** key on a machine. This KMS server will grant activation to all its
configured Generic-key subordinates that ask for it for a period of 180 days and
report your activations to Microsoft so you can pay for them. Basically, very
flexible and manageable license management with some setup required.

MAK keys are an alternative to this when you don't need or don't want a KMS
server. When paying for a MAK key you are buying a specific amount of
activations it can be used for. You can "spend" the key's activations wherever
and whenever you like. Very easy to use, requires no setup but could be hard to
keep track of.

## Regular Users
All this licensing crap surely doesn't mean anything to the regular user, does
it? Well.. yeah..

When activating Windows as all normal people do - using an activator - you don't
really pay attention to the tricks behind the scenes. You end up with an
activated system and that's it. Some more attentive users might notice that
during activation there are specific words and incantations thrown around,
including (but not limited to) spells like "installing product key",
"patching gatherosstate", "generating ticket", "activating Windows", 
"setting KMS server".

In this repository I will be trying to describe all the activation methods and
answer all questions that might arise from hearing those weird incantations
above. But first, we need to know what activation methods there even are.

### Types of Windows 10 Activation
For Windows 10 there are four main types of activation. Those are:

 * **Emulated KMS activation**
 * **KMS38**
 * **HWID / Digital License**
 * Buying it legally (lmao)

***Work in Progress***
