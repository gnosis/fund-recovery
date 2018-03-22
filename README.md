# Fund recovery
Recovery mechanisms for multi-signature wallets beyond backing up private keys.

## Background
On Ethereum, private keys are used to access accounts, sign messages etc. Basically once you lose access to your private key, you lost access to all funds stored with that account. There is absolutely no way to gain back access.
Users need to take care of backing up their recovery passphrase to a safe place themselves. Quite a significant amount of users loses this passphrase or does not back it up in the first place.

## Goals
### Recoverability
Offer a variety of options to enable users to recover their account. Users should be able to configure recovery options even for the case that the user lost their private keys.
### Usability / awareness
The user needs to understand how different recovery options work and that is it very important to configure them.
### Custody
Gnosis (or any other wallet provider) should not be able to take control over users’ accounts. 
### Security / identity
Obviously there should be no easy way to hijack the account of another person via recovery options. Only the person actually owning the account / Safe should be able to recover it.

## Misc
We have to differentiate between solutions where account to the Ethereum account is recovered and solution where access to the Safe contract is recovered. The Gnosis Safe smart contract allows to configure recovery extensions that can replace owners. That means, the Ethereum account is not recovered, but access to the Safe (including funds).
### Multiple owners
MultiSig wallets allow for setting a number of owners n. If less than n owners are required, the remaining owners could replace an owner in case they lost access.
This solution however requires at least 3 owners or owner devices (2 confirmations required for transactions). Since usually people do not own more than 2 devices (mobile phone + computer), it is a solution applicable in the Team Edition and not so much in the Personal Edition. 
### Recovery passphrase
Users need to back up their recovery passphrase themselves and make sure to keep it safe. This recovery option is the standard for Ethereum addresses and wallets right now. We should allow this for advanced users, however a less knowledgeable user should have different options. 
It would have several advantages, if the private key effectively never needs to leave the device. More advanced user however will most likely want the option to take the private key themselves.
### Biometric data
Instead of having a recovery passphrase that can be lost, how about using biometric data like the fingerprint, iris scan or Apple’s face ID for recovery which cannot be “lost” like passwords on a piece of paper.
The problem with this option is, that e.g. different fingerprint sensors can get quite fuzzy and not match exactly. If the user cuts themselves then there might be problems. Also, once biometric data of a person is exposed to the public, they would be no way to secure an account with it anymore since you cannot really change you fingerprint like you can change a password or switch an account.
Leverage existing password managers / keychains
iOS and Android both offer built-in features to store password via the keychain (iOS) and keystore/smart locks (Android) which user are used to already. We could leverage this to store the recovery passphrase on behalf of the user. Obviously this is only as secure as access to these keychains is. Some of these systems have been hacked before (e.g. Apple keychain hack).
The same goes for storing the recovery passphrase in password managers like 1Password and LastPass.
### Social recovery
Users could determine a group of friends that are enabled to recover access to the Gnosis Safe on behalf of the user. Only when all friends agree, the Safe owner is replaced.
The biggest problem with this solution is, that the group of friends could work together and steal access to the Safe from the owner by working together even if the owner did not ask them to. That is why ideally, the members of the group should not know who else is part of the group.
### Leveraging KYC procedures
Similar to how modern banks perform KYC procedures on new customers, Safe users could identify themselves to KYC providers in order to regain access to their funds. Users would however need to perform the procedure already once to set it up so the providers know about the identity behind an address.
### Paralysis proof / time lock recovery / last resort recovery
(Partly based on http://hackingdistributed.com/2018/01/18/paralysis-proofs/)
In case access to an account is lost, it can be marked as such. Also, the person marking it as lost needs to put in a deposit. Now a time period starts after which the account is replaced. During that time period the actual account owner could prove that the account is actually not lost by making a transaction. If so, the attacker loses the deposit which is transferred to the account.
