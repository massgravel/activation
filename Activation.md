# The Activation Process

Welcome to the `Activation Process` document. This will have some info on
Windows 10 activation processes.

# Scope

Windows activation processes differ based on the type of license installed. In
this document an attempt will be made to semi-comprehensively describe how the
activation occurs for a given license type.

# Activation Processes

Methods used for activation can be roughly divided into three types. Those are:

 * **Involving Microsoft**
 * **Indirectly involving Microsoft**
 * **Not involving Microsoft**

The correlation between license type and how it activates is as follows:

 * **Involving Microsoft**:
   * Retail
   * Volume:MAK
   * OEM:NSLP
   * OEM:DM
 * **Indirectly involving Microsoft**
   * Volume:GVLK
 * **Not involving Microsoft**:
   * OEM:SLP

First of all, it'd be nice to know what "activation" even does. In general, we
are trying to solicit a **license file** that will satisfy the **Software
Protection Platform** (SPP). When SPP is satisfied, the system is activated.

**License files** contain some information on the license: the type, issue date,
associated hardware ID (if applicable) and more.

Other than full  licenses, there are **grants** that are valid for a limited
time. After the time period specified in the grant expires your system will want
to renew it, prompting what is essentially a "reactivation" of the product.

Deposited licenses and grants can be found in `%windir%\System32\spp\store` and
`%programdata%\Microsoft\Windows\ClipSVC`.
Here's likely the simplest way to look through licenses in `tokens.dat`:

```sh
#!/usr/bin/env zsh
strings tokens.dat | grep -oP '<License[^>]*?>.*?</License>' > licenses
split -l1 licenses 'license-' && rm licenses
for l in license-*; do xmllint --format "$l" --output "$l.xml" && rm "$l"; done
# license-aa.xml, license-ab.xml, [...] will have all your licenses.
```

## Activation Involving Microsoft

For activation involving Microsoft their **activation servers** are contacted to
create and/or retrieve license files.

(The licensing and validation servers your installation uses can be checked with
`slmgr -dlv`)

The most common variant of this will be a **digital entitlement** (aka. "digital
license"). This type of license is retrieved through **any** of the following:

 * **Product key**
 * **Machine**
 * **Microsoft account**
 
All those above, except the **Machine** type (**TBV**) are subject to RIT and ROT related
effects.

### RIT and ROT

When the hardware ID for the machine for which a license is issued changes, the
license has to be **reissued**. There are two recozniged types of reissues:

 * Reissue **In-Tolerance**
 * Reissue **Out-of-Tolerance**

In-tolerance reissues guarantee that the license sticks through some number of minor hardware
changes. Out-of-tolerance reissues usually happen for drastic hardware changes, disk transfers
and MSA (Microsoft Account) transfers.

#### Reissue In-Tolerance

When the hardware changes only slightly (or is client-correctable, e.g. by adjusting for RAM)
a Reissue In-Tolerance is triggered and the license's Hardware ID is adjusted
to match the new one.

The "RIT limit", for how many times such a reissue can happen, is currently thought to be
unlimited.

#### Reissue Out-of-Tolerance

When a drastic hardware change is detected and the license no longer matches - a Reissue
Out-of-Tolerance is triggered. The process is roughly the same as for RIT, except the limit
for how many reissues can happen is much lower.

A reissue out-of-tolerance also happens when the same product key is installed on a
different machine, when the license store is moved to a different machine or via a 
Microsoft account.

The limit for Out-of-Tolerance reissues likely depends on the following:

 * Region (the license's assigned market)
 * Product (the licensed edition)
 * **Type of license** (Retail / OEM, tolerance a lot lower for OEM)

### Product key

When a valid Windows 10 product key is installed, activation will be attempted.
If your product key is valid and accepted by Microsoft, a digital license is
granted for your **machine** based on its **hardware ID**.

### Machine

When **any** valid Windows 10 product key is installed, activation servers are
contacted to try get a license for it. The activation server will notice your
**hardware ID** and, if it matches an existing digital license, will grant it to
you.

The key doesn't have to be valid in this case. Only its **type** matters. 

### Microsoft account

Microsoft accounts, being associated with the Microsoft Store, have information
on your Microsoft Store licenses - this includes Windows (*most* editions).

When you have a valid Retail (**TBV**) license for Windows, activation is granted
for new hardware - the computer you logged in with.

## Activation indirectly involving Microsoft

The only type of activation that (in theory at least) indirectly involves
Microsoft is for Volume:GVLK keys.

When a generic volume licensing key is installed, the configured KMS server is
contacted to provide the system with a grant for a specific period.
The activation period depends on the edition and is usually 180 days.

This **indirectly** involves Microsoft because, in a legit environment, the KMS
server reports to Microsoft.

## Activation not involving Microsoft

In the case of OEM:SLP licensing, the only basis for acquiring a valid license
file is a valid certificate and a BIOS marker.

Microsoft servers are **not** contacted here, instead the OEM's certificate
needs to be digitally signed by Microsoft.
