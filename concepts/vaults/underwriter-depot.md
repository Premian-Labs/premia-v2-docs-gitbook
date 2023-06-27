# Underwriter Depot

## _Introduction_

_The purpose of the creation of the underwiter vault is to migrate users from Premia V2 to Premia V3. The UnderwriterVault satisfies the ERC4626 vault standard and enables yearn compatibility._

### 1.1 General Overview and Functionality

{% hint style="info" %}
_The vault's purpose is to cluster liquidity that will be used to underwrite options at prices that are close to Deribit's. The depositor's liquidity will be used to underwrite calls and put options for a wide set of strikes and maturities._
{% endhint %}

_1.2 User Stories_

_• As a depositor, I want to deposit collateral into the vault so that I can receive shares that can later be redeemed for the premium and spread that is made by selling options to buyers in addition to my original deposit._

_• As a depositor, I want to be able to withdraw from a vault when there is capital available so that I can recover my collateral and realize the pro-rata P\&L from the time spent in the vault._

_• As a buyer, I want to receive a quote for an option purchase, so that I can know in advance what the premium will be for purchasing the options so that I can compare the cost with other outlets._

_• As a buyer, I want to purchase options from the vault by paying a premium so that I can receive long contracts._

_• As a vault operator, I want to settle all options up until the current time so that I increase the vault's liquidity / available assets, such that it will be available for depositors to withdraw or for buyers to purchase new options._

### Algorithmic Description

_In the following sections, we introduce the storage variables and their update rules upon external calls that are necessary to maintain the vault._

#### ERC4626 state variables

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

![](<../../.gitbook/assets/image (11).png>)![](<../../.gitbook/assets/image (15).png>)

![](<../../.gitbook/assets/image (10).png>)![](<../../.gitbook/assets/image (16).png>)![](<../../.gitbook/assets/image (7).png>)![](<../../.gitbook/assets/image (5).png>)![](<../../.gitbook/assets/image (14).png>)![](<../../.gitbook/assets/image (6).png>)![](<../../.gitbook/assets/image (2).png>)![](<../../.gitbook/assets/image (8).png>)![](<../../.gitbook/assets/image (4).png>)![](../../.gitbook/assets/image.png)![](<../../.gitbook/assets/image (17).png>)![](<../../.gitbook/assets/image (1).png>)![](<../../.gitbook/assets/image (12).png>)![](<../../.gitbook/assets/image (18).png>)![](<../../.gitbook/assets/image (9).png>)
