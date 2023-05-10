---
title: 'Troubleshooting Staking'
taxonomy:
    category:
        - Staking
    author:
        - 'The PIVX Team'
---

### Staking FAQ

[faqs]
[faq question="Why is staking inactive on my core wallet?"]
Please start by making sure you meet all the requirements listed on the [Staking](/staking) page. If this doesn't help, run the `getstakingstatus` command in the core wallet command line or debug console.  Any _false_ value should be investigated and most likely the cause for staking to be de-activated. *Note:* The _hot_ wallet in a cold staking setup has to be "_Unlocked for staking_"
[/faq]
[faq question="I have been staking XXX PIVs for YYY days and haven't received a reward yet. Is anything broken?"]
Verify the staking status of your core wallet or of your staking provider. If active, your next best option is to give it time, as the frequency on which a staker will receive rewards is completely random. A staking calculator can provide you with an expected return/staking frequency that can help manage your expectations:
* https://pivx.org/proof-of-stake
* https://toolbox.pivx.org/rewards
[/faq]
[faq question="I just received a staking reward and my staking balance is now down to zero. What is happening?"]
When a UTXO receives a stake, it will not be eligible for staking until it reaches 600 confirmations (approx. 10 hrs.) before it can be staked again.
[/faq]
[faq question="What is the Stake Split Threshold?"]
The _Stake Split Threshold_ defines how the output of a staking transaction will be split. It offers a way to split your balances into multiple UTXO, so that your stakes can be more regular. Its effect is more visible on larger (3,000 PIV+) balances.  Here's an example scenario for 1,900 PIV staked in a single UTXO.  If "_Stake Split Threshold_" is set to 2,000, the output for the staking transaction will be a single UTXO of 1,904 PIV. As that UTXO will need 600 confirmations to stake again, you will be staking 0 PIV for 10 hours.  That downtime in staking will repeat for the next stakes until the balance reaches 2,000 PIV.  If Stake Splitting Threshold is set to 500 (default value in Core Wallet), the output for the staking transaction will be 4 UTXO of 475.5 PIV. These 4 UTXO will need 600 confirmations to stake again, however, the next stake will only impact 3 of the 4 UTXO, so you will be staking 1,426 PIV while the staking transaction gets its 600 confirms.
[/faq]
[/faqs]

### Cold Staking FAQ
[faqs]
[faq question="I want to cold stake my PIVs but cannot maintain a hot wallet. Where do I find a staking provider?"]
Some members of the community offer to cold stake your PIVs on their wallet.  You can ask on Discord whether someone is willing to do it for you. There are also specialized service providers (such as [allnodes.com](https://help.allnodes.com/en/articles/3684105-how-to-stake-pivx-on-allnodes)) who offer this service for a small fee or for free.
[/faq]
[faq question="I have delegated my PIVs for Cold Staking to a third party. Can they access or spend my PIVs?"]
No. Cold Staking is a non-custodial. Your PIVs are safe in your cold/offline wallet and only you can access and spend them.
[/faq]
[faq question="How do I access/spend the PIVs that I have delegated for cold staking?"]
Just login to your cold wallet and spend them! It will break the cold staking for the UTXO you are spending, so if you want to stake the remainder of that UTXO you will need to put in place a new staking delegation.
[/faq]
[/faqs]

